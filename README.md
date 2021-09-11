# CP3108 Report

## Table of content
 - [Tasks](#tasks)
 - [Week 17](#week-17)
 - [Week 16](#week-16)
 - [Usage](#usage)

## Tasks
 - [x] Error handling with directory of PLY files
 - [x] Optimize reader in crate `ply_rs`
 - [ ] Install cargo instrument 
 - [ ] Make the png background transparent
 - [ ] Custimizable methods in `Filter and Transform` binary
 - [x] Display file name as the title of the window [see](#display-file-name-as-the-title-of-the-window)
 - [x] Print the `eye` and `at` information to the terminal [see](#print-the-eye-and-at-information-to-the-terminal)
 - [x] Adjust the default `eye` and `at` [see](#adjust-the-default-eye-and-at)
 - [ ] Customize the height and width of the window in `ply_view` [see](#customize-the-height-and-width-of-the-window-in-ply_view)

## Week 17

### Display file name as the title of the window
 * Problem: Cannot distinguish between multiple windows.
 * Solve: Added a field `title` into class `Points`:
    ```rust
    /// Class of Points containing all necessary metadata
    pub struct Points {
        /// Name of the points
        pub (crate) title: Option<String>,
        /// Data is a vector of type Point, storing all coordinate and colour data
        pub data: Vec<Point>,
        /// Stores the coordinate delta between the next and prev frames
        pub delta_pos_vector: Vec<Point3<f32>>,
        /// Stores the colour delta between the next and prev frames
        pub delta_colours: Vec<Point3<f32>>,
        /// Stores the next frame as a reference for mapping count and unmapped points
        pub reference_frame: Vec<Point>,
    }
    ```
  * Result: [see](https://drive.google.com/file/d/1W5XLVwHE8DLXqaMqnyRMlT2cMRL79CkD/view?usp=sharing)
### Print the `eye` and `at` information to the terminal
 * Problem: Gain runtime information of the positions of 'eye' and 'at'
 * Solve: [commit](https://github.com/hungkhoaitay/in-summer-we-render/commit/55d588f7c092b881db23f759a2ac6c836bd3aa85)
 * Tried native `relative_eq` in class `Point3` of crate `nalgebra` but the methods are private. Add dependency `approx` and do self compare.
### Adjust the default `eye` and `at`
 * Problem: The gap above is too large.
 * Solve:
   ```rust
   const DEFAULT_EYE: Point3<f32> = Point3::new(0.0f32, 500.0, 2500.0);
   const DEFAULT_AT: Point3<f32> = Point3::new(300.0f32, 800.0, 200.0);
   ```
   ```rust
   const DEFAULT_EYE: Point3<f32> = Point3::new(0.0f32, 500.0, 1800.0);
   const DEFAULT_AT: Point3<f32> = Point3::new(300.0f32, 500.0, 200.0);
   ```

### Customize the height and width of the window in `ply_view`
 * Problem: Able to do the same with `ply_to_png`.
 * Solve


## Week 16

### Reader optimization
 * Problem: The variable `key` keep cloning, detected by [weitsang](https://github.com/weitsang) using [cargo-instruments](https://github.com/cmyr/cargo-instruments).
 * Solve:
   * Original reading binary-file time: 450ms.
   * Here is the [changes](https://github.com/Fluci/ply-rs/compare/master...hungkhoaitay:master) that has been made.
   * Now the running time is reduced to be nearly 90ms :zany_face:


### Cargo instrument installation
Installed `brew` and `openssl` version x86. However, facing new [issue](https://github.com/cmyr/cargo-instruments/issues/50) :sweat_smile:

### Organising package
* Problem: The package is needed to be organised.
* Solve
  * Installed `tree` by `$ brew install tree` to present directoty.

### Error handling with directory of PLY files
 * Problem: Stop playing video when facing error with reading some files.

 * Solve
   * Handled the error in each file and print out error in the terminal
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

## Usage
```{.}
$ cargo run --release --bin ply_view -- -i /Users/hungkhoaitay/Library/plySource/binary_longdress/longdress_vox10_1223.ply
```
