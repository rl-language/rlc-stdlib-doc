# bounded_arg.rl

## cls BInt
```
 A integer with a max and min, so that
 enumerate will return the range of values
 between the two.
```

### Fields

* Int value

### Methods

* fun `equal(Int other)  -> Bool`
* fun `equal(BInt<min, max> other)  -> Bool`
* fun `less(BInt<min, max> other)  -> Bool`
* fun `less(Int other)  -> Bool`
* fun `greater(BInt<min, max> other)  -> Bool`
* fun `greater(Int other)  -> Bool`
* fun `greater_equal(BInt<min, max> other)  -> Bool`
* fun `greater_equal(Int other)  -> Bool`
* fun `less_equal(BInt<min, max> other)  -> Bool`
* fun `less_equal(Int other)  -> Bool`
* fun `assign(Int other) `
* fun `not_equal(Int other)  -> Bool`
* fun `not_equal(BInt<min, max> other)  -> Bool`
* fun `add(Int val)  -> BInt<min, max>`
* fun `add(BInt<min, max> other)  -> BInt<min, max>`
* fun `mul(BInt<min, max> other)  -> BInt<min, max>`
* fun `mul(Int val)  -> BInt<min, max>`
* fun `sub(BInt<min, max> other)  -> BInt<min, max>`
* fun `sub(Int val)  -> BInt<min, max>`


### Free functions

* fun `max<min : Int, max : Int>(BInt<min, max> l, BInt<min, max> r)  -> BInt<min, max>`
* fun `min<min : Int, max : Int>(BInt<min, max> l, BInt<min, max> r)  -> BInt<min, max>`
* fun `append_to_vector<min : Int, max : Int>(BInt<min, max> to_add, Vector<Byte> output) `
* fun `parse_from_vector<min : Int, max : Int>(BInt<min, max> to_add, Vector<Byte> output, Int index)  -> Bool`
* fun `append_to_string<min : Int, max : Int>(BInt<min, max> to_add, String output) `
* fun `parse_string<min : Int, max : Int>(BInt<min, max> to_add, String input, Int index)  -> Bool`
* fun `enumerate<min : Int, max : Int>(BInt<min, max> to_add, Vector<BInt<min, max>> output) `
