```rust
use std::str;
 
fn main() {
// 起始：Vec
let src1: Vec<char> = vec!['j','{','"','i','m','m','y','"','}'];
// 从 Vec 转换为String
let string1: String = src1.iter().collect::<String>();
// 从 Vec 转换为&str
let str1: &str = &src1.iter().collect::<String>();
// 从 Vec 转换为Vec
let byte1: Vec<u8> = src1.iter().map(|c| *c as u8).collect::<Vec<_>>();
//输出
println!("Vec<char>:{:?} | String:{:?}, str:{:?}, Vec<u8>:{:?}", src1, string1, str1, byte1);
 
// 起始：Vec 字节数组
// in rust, this is a slice
// b - byte, r - raw string, br - byte of raw string
let src2: Vec<u8> = br#"e{"ddie"}"#.to_vec();
// 从 Vec 转换为String
// from_utf8 以utf8方式转换
let string2: String = String::from_utf8(src2.clone()).unwrap();
// 从 Vec 转换为 &str
let str2: &str = str::from_utf8(&src2).unwrap();
// 从 Vec 转换为Vec
let char2: Vec<char> = src2.iter().map(|b| *b as char).collect::<Vec<_>>();
//输出
println!("Vec<u8>:{:?} | String:{:?}, str:{:?}, Vec<char>:{:?}", src2, string2, str2, char2);
 
// 起始为一个 String
let src3: String = String::from(r#"o{"livia"}"#);
// 直接变为一个&str
let str3: &str = &src3;
// 从 String 转换为Vec
let char3: Vec<char> = src3.chars().collect::<Vec<_>>();
// 从String转换为Vec
let byte3: Vec<u8> = src3.as_bytes().to_vec();
//Print
println!("String:{:?} | str:{:?}, Vec<char>:{:?}, Vec<u8>:{:?}", src3, str3, char3, byte3);
 
// 起点为 &str
let src4: &str = r#"g{'race'}"#;
// 从&str转换为String
let string4 = String::from(src4);
//从&str 转换为 Vech
let char4: Vec<char> = src4.chars().collect();
// 从 &str 转换为 Vec
let byte4: Vec<u8> = src4.as_bytes().to_vec();
//输出
println!("str:{:?} | String:{:?}, Vec<char>:{:?}, Vec<u8>:{:?}", src4, string4, char4, byte4);
}
```