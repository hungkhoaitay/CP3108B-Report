# CP3108 Report

 - [x] Error handling with directory of PLY files
 - [x] Optimize reader in crate `ply_rs`
 - [ ] Install cargo instrument 
 - [ ] Make the png background transparent
 - [ ] Custimizable methods in `Filter and Transform` binary

## Week 16

### Reader optimization
- Original reading binary-file time: 450ms.
- Here is the [changes](https://github.com/Fluci/ply-rs/compare/master...hungkhoaitay:master) that has been made.
- Now the running time is reduced to be nearly 90ms :zany_face:


### Cargo instrument installation
Installed `brew` and `openssl` version x86. However, facing new [issue](https://github.com/cmyr/cargo-instruments/issues/50) :sweat_smile:

### Organising package
- Installed `tree` by `$ brew install tree`

### Error handling with directory of PLY files
* Continuously play even when facing error with reading some files.
* Different error handling:
   * With file with appropriate extension but have empty content:
        ```
        Problem with reading file:
            Unable to read the header of the input: /Users/hungkhoaitay/Library/plySource/binary_longdress/error_file.ply
        ```
   * With file with inappropriate extension (not `.ply`):
        ```
        Problem with reading file:
            Extension of file: /Users/hungkhoaitay/Library/plySource/binary_longdress/error_file.txt expected to be .ply
        ```

