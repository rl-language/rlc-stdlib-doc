# to_byte_vector.rl


### Free functions

* fun `append_to_vector(Int to_add, Vector<Byte> output) `
* fun `append_to_vector(Float to_add, Vector<Byte> output) `
* fun `append_to_vector(Bool to_add, Vector<Byte> output) `
* fun `append_to_vector(Byte to_add, Vector<Byte> output) `
* fun `append_to_vector<T>(Vector<T> to_add, Vector<Byte> output) `
* fun `append_to_vector<T, X : Int>(T[X] to_add, Vector<Byte> output) `
* fun `append_to_byte_vector<T>(T to_convert, Vector<Byte> out) `
* fun `as_byte_vector<T>(T to_convert)  -> Vector<Byte>`
* fun `parse_from_vector(Int result, Vector<Byte> input, Int index)  -> Bool`
* fun `parse_from_vector(Float result, Vector<Byte> input, Int index)  -> Bool`
* fun `parse_from_vector(Bool result, Vector<Byte> input, Int index)  -> Bool`
* fun `parse_from_vector(Byte result, Vector<Byte> input, Int index)  -> Bool`
* fun `parse_from_vector<T>(Vector<T> output, Vector<Byte> input, Int index)  -> Bool`
* fun `parse_from_vector<T, X : Int>(T[X] to_add, Vector<Byte> input, Int index)  -> Bool`
* fun `from_byte_vector<T>(T result, Vector<Byte> input)  -> Bool`
* fun `from_byte_vector<T>(T result, Vector<Byte> input, Int read_bytes)  -> Bool`
