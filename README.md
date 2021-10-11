## Table of content
- [Table of content](#table-of-content)
- [Task](#task)
- [Week 20](#week-20)
  - [Cargo instruments](#cargo-instruments)
  - [Clipboard initialize](#clipboard-initialize)
  - [Refactoring part 3: Fail](#refactoring-part-3-fail)
- [Week 19](#week-19)
  - [Refactoring part 2](#refactoring-part-2)
  - [Information print (GUI)](#information-print-gui)
  - [Keyboard Input (Draft)](#keyboard-input-draft)
- [Week 18](#week-18)
  - [Fix display file name as the title of the window](#fix-display-file-name-as-the-title-of-the-window)
  - [Display file name as the title of the window for PLY-directory](#display-file-name-as-the-title-of-the-window-for-ply-directory)
  - [Autofill output of `ply_to_png`](#autofill-output-of-ply_to_png)
  - [Organizing package](#organizing-package)
- [Week 17](#week-17)
  - [Display file name as the title of the window](#display-file-name-as-the-title-of-the-window)
  - [Print the `eye` and `at` information to the terminal](#print-the-eye-and-at-information-to-the-terminal)
  - [Adjust the default `eye` and `at`](#adjust-the-default-eye-and-at)
  - [Cargo instrument installation](#cargo-instrument-installation)
  - [Customize the height and width of the window in `ply_view`](#customize-the-height-and-width-of-the-window-in-ply_view)
- [Week 16](#week-16)
  - [Reader optimization](#reader-optimization)
  - [Error handling with directory of PLY files](#error-handling-with-directory-of-ply-files)
- [Usages](#usages)

## Task
 * [ ] Make the png background transparent
 * [ ] Customizable methods in `Filter and Transform` binary
 * [ ] Information print
 * [ ] Cargo instruments

## Week 20

### Cargo instruments
* [Issue](https://github.com/hungkhoaitay/in-summer-we-render/issues/13)

### Clipboard initialize
* [Pull request](https://github.com/hungkhoaitay/in-summer-we-render/pull/14)

### Refactoring part 3: Fail

## Week 19

### Refactoring part 2

  * [Pull request](https://github.com/hungkhoaitay/in-summer-we-render/pull/8/files)
  * Results:
    ```
    src
    ├── bin
    │   ├── ply_fat.rs
    │   ├── ply_interpolate.rs
    │   ├── ply_to_ply.rs
    │   ├── ply_to_png.rs
    │   ├── ply_view.rs
    │   └── test.rs
    ├── examples
    ├── io
    │   ├── mod.rs
    │   ├── reader.rs
    │   └── writer.rs
    ├── lib.rs
    ├── ply.rs
    ├── ply_dir.rs
    ├── pointcloud
    │   ├── color.rs
    │   ├── coordinate.rs
    │   ├── mod.rs
    │   ├── params.rs
    │   ├── point.rs
    │   └── points.rs
    ├── processing
    │   ├── filter_and_transform
    │   │   ├── fat.rs
    │   │   ├── filter.rs
    │   │   ├── mod.rs
    │   │   └── transform.rs
    │   ├── interpolate.rs
    │   ├── interpolate_controller.rs
    │   └── mod.rs
    └── render
        ├── gui.rs
        ├── gui_states.rs
        ├── mod.rs
        └── renderer.rs
    ```

### Information print (GUI)
  * [Pull request](https://github.com/hungkhoaitay/in-summer-we-render/pull/7/files)
  * Using feature `conrod` of dependency `kiss3d`
  * [Result](https://drive.google.com/drive/folders/1-PPZ7oOJJddoioYzD0v60zmD_nV0n6Qd?usp=sharing)

### Keyboard Input (Draft)
  * [Pull request](https://github.com/hungkhoaitay/in-summer-we-render/pull/9/files)
  * Using module `event` in feature `conrod` of dependency `kiss3d`
  * [Result for press 'I'](https://drive.google.com/file/d/1-qDjGRFglghwwr1-zXe0Cj6yjta2MkvV/view?usp=sharing) 
  * [Result for press 'Space'](https://drive.google.com/file/d/1-phOfkROmKJmKsfnPPUWiJrh7kqszpfH/view?usp=sharing)

## Week 18

### Fix display file name as the title of the window

  * Fix struct `Points`
    ```rust
    /// Class of Points containing all necessary metadata
    pub struct Points {
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
    
 * New struct `Ply`
    ```rust
    pub struct Ply {
        title: Option<PathBuf>,
        points: Points,
    }
    ```
    
 * [Pull request](https://github.com/hungkhoaitay/in-summer-we-render/pull/5/files)

### Display file name as the title of the window for PLY-directory

 * [Pull request](https://github.com/hungkhoaitay/in-summer-we-render/pull/5/files)
 * Results:
   * <- Command:
   ```
   $ ply_view -i $plySource/binary_longdress/ -b=100,100,100
   ```
   * -> [Result](https://drive.google.com/file/d/1Wcc_N08JRkk7fbg0ss2fvFMaI3o73g5n/view?usp=sharing)
 
### Autofill output of `ply_to_png`

 * [Pull request](https://github.com/hungkhoaitay/in-summer-we-render/pull/5/files)
 * Results:
   * <- Command:
   ```
   $ ply_to_png -- -i $plySource/binary_longdress/longdress_vox10_1223.ply
   ```
   * -> Result
   ```
    Finished release [optimized + debuginfo] target(s) in 0.32s
     Running `target/release/ply_to_png -i /Users/hungkhoaitay/Library/plySource//binary_longdress/longdress_vox10_1223.ply`
   Image saved to "longdress_vox10_1223.png"
   ```
   * -> Command:
   ```
   $ ply_to_ply -- -i $plySource/binary_longdress/longdress_vox10_1223.ply | ply_to_png
   ```
   * <- Result
   ```
    Blocking waiting for file lock on package cache
    Blocking waiting for file lock on package cache
    Blocking waiting for file lock on package cache
    Blocking waiting for file lock on package cache
    Blocking waiting for file lock on package cache
    Blocking waiting for file lock on package cache
    Blocking waiting for file lock on build directory
    Finished release [optimized + debuginfo] target(s) in 0.39s
     Running `target/release/ply_to_ply -i /Users/hungkhoaitay/Library/plySource//binary_longdress/longdress_vox10_1223.ply`
    Finished release [optimized + debuginfo] target(s) in 0.42s
     Running `target/release/ply_to_png`
   Image saved to "output.png"
   ```

### Organizing package

* Problem: The package is needed to be organized.
* Solve: Installed `tree` by `$ brew install tree` to present directory.
* Result:
  ```
  src
  ├── bin
  │   ├── ply_fat.rs
  │   ├── ply_interpolate.rs
  │   ├── ply_to_ply.rs
  │   ├── ply_to_png.rs
  │   ├── ply_view.rs
  │   └── test.rs
  ├── examples
  ├── lib.rs
  ├── materials
  │   ├── color.rs
  │   ├── coordinate.rs
  │   ├── mod.rs
  │   ├── params.rs
  │   ├── ply.rs
  │   ├── ply_dir.rs
  │   ├── point.rs
  │   └── points.rs
  ├── methods
  │   ├── filter.rs
  │   ├── mod.rs
  │   └── transform.rs
  └── tool
      ├── fat.rs
      ├── interpolate.rs
      ├── interpolate_controller.rs
      ├── mod.rs
      ├── reader.rs
      ├── renderer.rs
      └── writer.rs
  ```

* Note: Haven't tested interpolate yet!

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
  * [Result](https://drive.google.com/file/d/1W5XLVwHE8DLXqaMqnyRMlT2cMRL79CkD/view?usp=sharing)

### Print the `eye` and `at` information to the terminal

 * Problem: Gain runtime information of the positions of 'eye' and 'at'
 * Solve: [commit](https://github.com/hungkhoaitay/in-summer-we-render/commit/55d588f7c092b881db23f759a2ac6c836bd3aa85)
 * Tried native `relative_eq` in class `Point3` of crate `nalgebra` but the methods are private. Add dependency `approx` and do self compare.
 * Detect changes with `eye` and `at` but not from the `window`.
 * [Result](https://drive.google.com/file/d/1NQWOk9PIPNAV4QWaZ35VoaOqXL_kiIL3/view?usp=sharing)

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
 * [Result](https://drive.google.com/file/d/1DH8ischKss6y2wBDPCiBBHXB6KqXpdlf/view?usp=sharing)

### Cargo instrument installation
  * Solve
    * Installed `brew` Intel version and installed `cargo-instruments` via it successfully.
    * [Installation of `brew` Intel version](https://stackoverflow.com/questions/64951024/how-can-i-run-two-isolated-installations-of-homebrew)
    * [Unknown Error solved](https://github.com/Homebrew/brew/issues/10368)


### Customize the height and width of the window in `ply_view`

 * Problem: Able to do the same with `ply_to_png`.
 * Solve: [Pull request](https://github.com/hungkhoaitay/in-summer-we-render/pull/4/files)


## Week 16

### Reader optimization

 * Problem: The variable `key` keep cloning, detected by [weitsang](https://github.com/weitsang) using [cargo-instruments](https://github.com/cmyr/cargo-instruments).
 * Solve:
   * Original reading binary-file time: __450ms__ :sweat_smile:
   * Here is the [changes](https://github.com/Fluci/ply-rs/compare/master...hungkhoaitay:master) that has been made.
   * Now the running time is reduced to be nearly __90ms__ :zany_face:

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

## Usages
```{.}
$ cargo run --release --bin ply_view -- -i $plySource/binary_longdress/longdress_vox10_1223.ply
```
```
$ cargo run --release --bin ply_fat -- -i $plySource/binary_longdress/longdress_vox10_1223.ply --filter upper_half -t all_red | cargo run --release --bin ply_view
```
```
$ cargo run --release --bin ply_to_png -- -i $plySource/binary_longdress/longdress_vox10_1223.ply -x 600 -w 400 -h 800 -o ouput.png
```
```
$ cargo run --release --bin ply_to_ply -- -i $plySource/binary_longdress/longdress_vox10_1223.ply –f binary –o output.ply
```
