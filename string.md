# string.rl

## cls String
```
 a c style string, composed of a series of ascii characters
 terminated by a null terminator.
```

### Fields


### Methods

* fun `init() `
```
 asd
```
* fun `append(Byte b) `
```
 append the byte b, interpreted as a ascii
 character to the string
```
* fun `get(Int index)  -> ref Byte`
* fun `substring_matches(StringLiteral lit, Int pos)  -> Bool`
* fun `size()  -> Int`
* fun `count(Byte b)  -> Int`
* fun `append(StringLiteral str) `
* fun `append(String str) `
* fun `add(String other)  -> String`
* fun `equal(StringLiteral other)  -> Bool`
* fun `equal(String other)  -> Bool`
* fun `not_equal(String other)  -> Bool`
* fun `not_equal(StringLiteral other)  -> Bool`
* fun `drop_back(Int quantity) `
* fun `back()  -> ref Byte`
* fun `reverse() `
* fun `to_indented_lines()  -> String`


### Free functions

* fun `s(StringLiteral literal)  -> String`
* fun `append_to_string(StringLiteral x, String output) `
* fun `load_file(String file_name, String out)  -> Bool`
* fun `append_to_string(Int x, String output) `
* fun `append_to_string(Byte x, String output) `
* fun `append_to_string(Float x, String output) `
* fun `append_to_string(Bool x, String output) `
* fun `append_to_string<T, X : Int>(T[X] to_add, String output) `
* fun `append_to_string<T>(Vector<T> to_add, String output) `
* fun `append_to_string<T, dim : Int>(BoundedVector<T, dim> to_add, String output) `
* fun `to_string<T>(T to_stringyfi, String output) `
* fun `to_string<T>(T to_stringyfi)  -> String`
* fun `is_space(Byte b)  -> Bool`
* fun `is_alphanumeric(Byte b)  -> Bool`
* fun `is_open_paren(Byte b)  -> Bool`
* fun `is_close_paren(Byte b)  -> Bool`
* fun `parse_string(Int result, String buffer, Int index)  -> Bool`
* fun `parse_string(Byte result, String buffer, Int index)  -> Bool`
* fun `parse_string(Float result, String buffer, Int index)  -> Bool`
* fun `lenght(StringLiteral literal)  -> Int`
* fun `parse_string(Bool result, String buffer, Int index)  -> Bool`
* fun `parse_string<T, X : Int>(T[X] result, String buffer, Int index)  -> Bool`
* fun `parse_string<T>(Vector<T> result, String buffer, Int index)  -> Bool`
* fun `parse_string<T, x : Int>(BoundedVector<T, x> result, String buffer, Int index)  -> Bool`
* fun `from_string<T>(T result, String buffer)  -> Bool`
* fun `from_string<T>(T result, String buffer, Int index)  -> Bool`
```
 given a String *buffer* and a offset into that string index,
 parses buffer starting from *index* and uses those information
 to set the value of *result*.
```
