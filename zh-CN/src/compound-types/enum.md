# æä¸¾ Enum
1. ðð å¨åå»ºæä¸¾æ¶ï¼ä½ å¯ä»¥ä½¿ç¨æ¾å¼çæ´æ°è®¾å®æä¸¾æåçå¼ã

```rust,editable

// ä¿®å¤éè¯¯
enum Number {
    Zero,
    One,
    Two,
}

enum Number1 {
    Zero = 0,
    One,
    Two,
}

// Cè¯­è¨é£æ ¼çæä¸¾å®ä¹
enum Number2 {
    Zero = 0.0,
    One = 1.0,
    Two = 2.0,
}


fn main() {
    // éè¿ `as` å¯ä»¥å°æä¸¾å¼å¼ºè½¬ä¸ºæ´æ°ç±»å
    assert_eq!(Number::One, Number1::One);
    assert_eq!(Number1::One, Number2::One);
} 
```

2. ð æä¸¾æåå¯ä»¥ææåç§ç±»åçå¼
```rust,editable

// å¡«ç©º
enum Message {
    Quit,
    Move { x: i32, y: i32 },
    Write(String),
    ChangeColor(i32, i32, i32),
}

fn main() {
    let msg1 = Message::Move{__}; // ä½¿ç¨x = 1, y = 2 æ¥åå§å
    let msg2 = Message::Write(__); // ä½¿ç¨ "hello, world!" æ¥åå§å
} 
```

3. ðð æä¸¾æåä¸­çå¼å¯ä»¥ä½¿ç¨æ¨¡å¼å¹éæ¥è·å
```rust,editable

// ä»å¡«ç©ºå¹¶ä¿®å¤éè¯¯
enum Message {
    Quit,
    Move { x: i32, y: i32 },
    Write(String),
    ChangeColor(i32, i32, i32),
}

fn main() {
    let msg = Message::Move{x: 1, y: 2};

    if let Message::Move{__} = msg {
        assert_eq!(a, b);
    } else {
        panic!("ä¸è¦è®©è¿è¡ä»£ç è¿è¡ï¼");
    }
} 
```

4. ðð ä½¿ç¨æä¸¾å¯¹ç±»åè¿è¡åä¸å

```rust,editable

// å¡«ç©ºï¼å¹¶ä¿®å¤éè¯¯
enum Message {
    Quit,
    Move { x: i32, y: i32 },
    Write(String),
    ChangeColor(i32, i32, i32),
}

fn main() {
    let msgs: __ = [
        Message::Quit,
        Message::Move{x:1, y:3},
        Message::ChangeColor(255,255,0)
    ];

    for msg in msgs {
        show_message(msg)
    }
} 

fn show_message(msg: Message) {
    println!("{}", msg);
}
```

5. ðð Rust ä¸­æ²¡æ `null`ï¼æä»¬éè¿ `Option<T>` æä¸¾æ¥å¤çå¼ä¸ºç©ºçæåµ
```rust,editable

// å¡«ç©ºè®© `println` è¾åºï¼åæ¶æ·»å ä¸äºä»£ç ä¸è¦è®©æåä¸è¡ç `panic` æ§è¡å°
fn main() {
    let five = Some(5);
    let six = plus_one(five);
    let none = plus_one(None);

    if let __ = six {
        println!("{}", n)
    } 
        
    panic!("ä¸è¦è®©è¿è¡ä»£ç è¿è¡ï¼");
} 

fn plus_one(x: Option<i32>) -> Option<i32> {
    match x {
        __ => None,
        __ => Some(i + 1),
    }
}
```


6. ðððð ä½¿ç¨æä¸¾æ¥å®ç°é¾è¡¨.

```rust,editable

// å¡«ç©ºï¼è®©ä»£ç è¿è¡
use crate::List::*;

enum List {
    // Cons: é¾è¡¨ä¸­åå«æå¼çèç¹ï¼èç¹æ¯åç»ç±»åï¼ç¬¬ä¸ä¸ªåç´ æ¯èç¹çå¼ï¼ç¬¬äºä¸ªåç´ æ¯æåä¸ä¸ä¸ªèç¹çæé
    Cons(u32, Box<List>),
    // Nil: é¾è¡¨ä¸­çæåä¸ä¸ªèç¹ï¼ç¨äºè¯´æé¾è¡¨çç»æ
    Nil,
}

// ä¸ºæä¸¾å®ç°ä¸äºæ¹æ³
impl List {
    // åå»ºç©ºçé¾è¡¨
    fn new() -> List {
        // å ä¸ºæ²¡æèç¹ï¼æä»¥ç´æ¥è¿å Nil èç¹
        // æä¸¾æå Nil çç±»åæ¯ List
        Nil
    }

    // å¨èçé¾è¡¨åé¢æ°å¢ä¸ä¸ªèç¹ï¼å¹¶è¿åæ°çé¾è¡¨
    fn prepend(self, elem: u32) -> __ {
        Cons(elem, Box::new(self))
    }

    // è¿åé¾è¡¨çé¿åº¦
    fn len(&self) -> u32 {
        match *self {
            // è¿éæä»¬ä¸è½æ¿èµ° tail çæææï¼å æ­¤éè¦è·åå®çå¼ç¨
            Cons(_, __ tail) => 1 + tail.len(),
            // ç©ºé¾è¡¨çé¿åº¦ä¸º 0
            Nil => 0
        }
    }

    // è¿åé¾è¡¨çå­ç¬¦ä¸²è¡¨ç°å½¢å¼ï¼ç¨äºæå°è¾åº
    fn stringify(&self) -> String {
        match *self {
            Cons(head, ref tail) => {
                // éå½çæå­ç¬¦ä¸²
                format!("{}, {}", head, tail.__())
            },
            Nil => {
                format!("Nil")
            },
        }
    }
}

fn main() {
    // åå»ºä¸ä¸ªæ°çé¾è¡¨(ä¹æ¯ç©ºç)
    let mut list = List::new();

    // æ·»å ä¸äºåç´ 
    list = list.prepend(1);
    list = list.prepend(2);
    list = list.prepend(3);

    // æå°åè¡¨çå½åç¶æ
    println!("é¾è¡¨çé¿åº¦æ¯: {}", list.len());
    println!("{}", list.stringify());
}
```

> ä½ å¯ä»¥å¨[è¿é](https://github.com/sunface/rust-by-practice/blob/master/solutions/compound-types/enum.md)æ¾å°ç­æ¡(å¨ solutions è·¯å¾ä¸) 