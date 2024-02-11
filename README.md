[![Gem Version](https://badge.fury.io/rb/dmtx.svg)](https://badge.fury.io/rb/dmtx)
[![build](https://github.com/mtgrosser/dmtx/actions/workflows/build.yml/badge.svg)](https://github.com/mtgrosser/dmtx/actions/workflows/build.yml)

# dmtx
Pure Ruby Data Matrix generator

## Installation

In your Gemfile:

```ruby
gem 'dmtx'
```

## Usage

```ruby
dmtx = Dmtx::DataMatrix.new('Chunky Bacon')

puts dmtx.to_s

██  ██  ██  ██  ██  ██  ██  ██  
██  ██████  ██  ██          ████
████  ██  ██████████████  ████  
██    ████  ██  ██████  ██    ██
██    ████    ██  ██    ██████  
██  ██████  ████████████    ████
██    ██  ████    ██    ██      
██      ██        ██████  ██  ██
██  ████      ████  ████████    
██  ████    ██    ████  ██  ████
████          ██████████████    
██  ██  ████  ████  ██  ██  ████
██    ████  ██    ██            
████████    ██  ██      ████  ██
██  ██  ██████    ██████    ██  
████████████████████████████████

dmtx.width
=> 16

dmtx.height
=> 16

dmtx.encoding
=> :ascii

dmtx.encoded_message
=> [68, 105, 118, 111, 108, 122, 33, 67, 98, 100, 112, 111,
    62, 103, 49, 93, 99, 53, 117, 202, 250, 186, 232, 14]

# Generate SVG
dmtx.to_svg
=> "<svg xmlns= ..."

# SVG default options
dmtx.to_svg(dim: 256, pad: 2, bgcolor: nil, color: '#000')

# Generate PNG with given module pixel size
dmtx.to_png
=> <ChunkyPNG::Image 160x160>

# raw PNG data
dmtx.to_png.to_s
=> "\x89PNG..."

# PNG default options
dmtx.to_png(mod: 8, pad: 2, bgcolor: nil, color: '#000')

# Integer representation
dmtx.to_i
=> 77194835539484717974890203635482091341863808501307723137647139603919014133759

# Binary representation
dmtx.to_i.to_s(2)
=> "1010101010101010
    1011101010000011
    1101011111110110
    1001101011101001
    1001100101001110
    1011101111110011
    1001011001001000
    1000100001110101
    1011000110111100
    1011001001101011
    1100000111111100
    1010110110101011
    1001101001000000
    1111001010001101
    1010111001110010
    1111111111111111"

# Choose encoding
Dmtx::DataMatrix.new('Chunky Bacon', encoding: :txt)

# GS1 DataMatrix
Dmtx::DataMatrix.new("\x1d01095011010209171719050810ABCD1234\x1d2110", encoding: :gs1)
