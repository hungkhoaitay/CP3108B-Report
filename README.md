# CP3108 Report

 - [ ] Optimize reader in crate `ply_rs`
 - [ ] Install cargo instrument 
 - [ ] Make the png background transparent
 - [ ] Custimizable methods in `Filter and Transform` binary

## Week 16

### Reader optimization
- [Changes made](https://github.com/Fluci/ply-rs/compare/master...hungkhoaitay:master)
- Highlight:

Original | Optimal
------------ | -------------
`fn set_property(&mut self, _property_name: String, _property: Property) {`{:.rust} | `fn set_property(&mut self, _property_name: &String, _property: Property) {`{:.rust}
Content in the first column | Content in the second column


### Cargo instrument installation
Installed `brew` and `openssl` version x86. However, facing new [Issue](https://github.com/cmyr/cargo-instruments/issues/50)
