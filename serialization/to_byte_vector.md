# to_byte_vector.rl


### Free functions

* fun `append_to_vector(Int to_add, Vector<Byte> output) `
* fun `append_to_vector(Float to_add, Vector<Byte> output) `
* fun `append_to_vector(Bool to_add, Vector<Byte> output) `
* fun `append_to_vector(Byte to_add, Vector<Byte> output) `
* fun `append_to_vector<T>(Vector<T> to_add, Vector<Byte> output) `
* fun `append_to_vector<T, X : Int>(T[X] to_add, Vector<Byte> output) `
* fun `append_to_byte_vector<T>(T to_convert, Vector<Byte> out) `
```
 converts `to_convert` to a sequence of bytes and adds it
 to `out`.
```
* fun `as_byte_vector<T>(T to_convert)  -> Vector<Byte>`
```
 converts `to_convert` to a sequence of bytes 
```
* fun `parse_from_vector(Int result, Vector<Byte> input, Int index)  -> Bool`
* fun `parse_from_vector(Float result, Vector<Byte> input, Int index)  -> Bool`
* fun `parse_from_vector(Bool result, Vector<Byte> input, Int index)  -> Bool`
* fun `parse_from_vector(Byte result, Vector<Byte> input, Int index)  -> Bool`
* fun `parse_from_vector<T>(Vector<T> output, Vector<Byte> input, Int index)  -> Bool`
* fun `parse_from_vector<T, X : Int>(T[X] to_add, Vector<Byte> input, Int index)  -> Bool`
* fun `from_byte_vector<T>(T result, Vector<Byte> input)  -> Bool`
```
 converts the bytes in `input` into a T and 
 assigns the value to `result`. Returns false if the conversion failed.
```
* fun `from_byte_vector<T>(T result, Vector<Byte> input, Int read_bytes)  -> Bool`
```
 converts the bytes in `input` starting at `read_bytes` into a T and 
 assigns the value to `result`. Returns false if the conversion failed.
 read_bytes is advanced up to the index of the first bytes not used to
 parse `result`
```
## trait ByteVectorSerializable
```
 Trait that must be implemented by a type 
 to override the standad way it is added to
 a vector of bytes
```
* fun `append_to_vector(T to_add, Vector<Byte> output) `

## trait ByteVectorParsable
```
 Trait that can be implemented to override the default conversion
 from a array of bytes to a object.
 It must be implemented if the trait has implemented ByteVectorSerializable
```
* fun `parse_from_vector(T result, Vector<Byte> input, Int index)  -> Bool`

