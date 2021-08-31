# CP3108 Report

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
Installed `brew` and `openssl` version x86. However, facing new [issue](https://github.com/cmyr/cargo-instruments/issues/50)
