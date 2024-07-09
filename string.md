# string.rl

## cls String
```
 a c style string, composed of a series of ascii characters
 terminated by a null terminator. If the string changes, it 
 may be reallocated, causing all references to its 
 characters to be invalidated.
```

### Fields


### Methods

* fun `init() `
* fun `append(Byte b) `
```
 append the byte b, interpreted as a ascii
 character to the string
```
* fun `get(Int index)  -> ref Byte`
```
 returns a reference to the character
 at the `index` location
```
* fun `substring_matches(StringLiteral lit, Int pos)  -> Bool`
```
 returns true if the current string contains the
 string `lit` starting from the character at `pos`
```
* fun `size()  -> Int`
```
 returns the size of the string, excluding
 the null terminator
```
* fun `count(Byte b)  -> Int`
```
 returns the number of occurences
 a certain character appears in the string
```
* fun `append(StringLiteral str) `
```
 appens `str` to the current string
```
* fun `append(String str) `
```
 appens `str` to the current string
```
* fun `add(String other)  -> String`
```
 returns the concatenation of this
 string and `other`, without modifying
 this string.
```
* fun `equal(StringLiteral other)  -> Bool`
```
 returns true if every character of this
 string is equal to every character of
 the `other` string
```
* fun `equal(String other)  -> Bool`
```
 returns true if every character of this
 string is equal to every character of
 the `other` string
```
* fun `not_equal(String other)  -> Bool`
* fun `not_equal(StringLiteral other)  -> Bool`
* fun `drop_back(Int quantity) `
```
 removes `quantity` characters from the
 end of the string
```
* fun `back()  -> ref Byte`
```
 returns a reference the last character before 
 the null terminator of the string
```
* fun `reverse() `
```
 reverses inplace the string
```
* fun `to_indented_lines()  -> String`
```
 returns a string such that every parantesys
 in this string generates a new line indented
 as many times as the number of 
 parentesys not yet closed
```


### Free functions

* fun `s(StringLiteral literal)  -> String`
```
 transforms a string literal into a String
 ex: let str = "hey"s.add(" bye")
```
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
```
 convert a object type into a string 
```
* fun `is_space(Byte b)  -> Bool`
* fun `is_alphanumeric(Byte b)  -> Bool`
* fun `is_open_paren(Byte b)  -> Bool`
* fun `is_close_paren(Byte b)  -> Bool`
* fun `parse_string(Int result, String buffer, Int index)  -> Bool`
* fun `parse_string(Byte result, String buffer, Int index)  -> Bool`
* fun `parse_string(Float result, String buffer, Int index)  -> Bool`
* fun `length(StringLiteral literal)  -> Int`
```
 returns the length of a string literal
```
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
## trait StringSerializable
```
 Trait that can be implemented by a type to override
 the regular conversion to string for that type.
```
* fun `append_to_string(T to_add, String output) `

## trait CustomGetTypeName
```
 Trait that can be implemented by a type to override
 which name is displayed in serialization of alternative 
 types
```
* fun `get_type_name(T to_add)  -> StringLiteral`

## trait StringParsable
```
 Trait that must be implemented to allow to convert
 string into a type when StringSerializable has been
 overwritten as well.
```
* fun `parse_string(T result, String buffer, Int index)  -> Bool`

