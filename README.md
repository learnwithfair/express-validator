# VALIDATION-WITH-EXPRESS-VALIDATOR

[![Youtube][youtube-shield]][youtube-url]
[![Facebook][facebook-shield]][facebook-url]
[![Instagram][instagram-shield]][instagram-url]
[![LinkedIn][linkedin-shield]][linkedin-url]

Thanks for visiting my GitHub account!

<img src ="screenshot/icon.png" height = "200px" width = "200px"/> **Express-validator** is a set of express.js middlewares that wraps the extensive collection of validators and sanitizers offered by validator.js.

It allows you to combine them in many ways so that, you can validate and sanitize your express requests and offers tools to determine if the request is valid or not, which data was matched according to your validators, and so on. [see-more](https://express-validator.github.io/docs/)

### [Code-Example](https://github.com/learnwithfair/mern-ecommerce-electro-master)

## Source Code 
[download](https://mega.nz/file/xKNl3bib#9NOgw1YEr6uL8z_4Ez56cagl4cnPeoY6bGyGaj4hdwc)

## How to use this project

- step 1: `npm install express-validator`
- step 2: create the sanitation rules that you want to use for validating the data

### Example of Sanitation Rules

```js
// validation/auth.js
const { check } = require("express-validator");

exports.userRegistrationValidator = [
  check("name")
    .trim()
    .notEmpty()
    .withMessage("Name is missing")
    .isLength({ min: 5, max: 31 })
    .withMessage("name must have at least 5 characters")
    .isLength({ max: 31 })
    .withMessage("name can have maximum 31characters"),
  check("email")
    .trim()
    .notEmpty()
    .withMessage("Email is missing")
    .isEmail()
    .withMessage("Not a valid email"),
  check("password")
    .trim()
    .notEmpty()
    .withMessage("Password is missing")
    .isLength({ min: 5 })
    .withMessage("password must have at least 5 characters"),
  check("dob")
    .trim()
    .notEmpty()
    .withMessage("dob is missing")
    .isISO8601()
    .toDate()
    .withMessage("Not a valid dob"),
  check("image")
    .optional()
    .isString()
    .withMessage("User image must be a string"),
];

exports.userLoginValidator = [
  check("email")
    .trim()
    .notEmpty()
    .withMessage("Email is missing")
    .isEmail()
    .withMessage("Not a valid email"),
  check("password")
    .trim()
    .notEmpty()
    .withMessage("Password is missing")
    .isLength({ min: 5 })
    .withMessage("password must have at least 5 characters"),
];

const validateUserPasswordUpdate = [
  check("email")
    .trim()
    .notEmpty()
    .withMessage("Email is required")
    .isEmail()
    .withMessage("Invalid email address"),
  check("oldPassword")
    .trim()
    .notEmpty()
    .withMessage("Old Password is required")
    .isLength({ min: 6 })
    .withMessage("Password should be at least 6 characters long"),
  check("newPassword")
    .trim()
    .notEmpty()
    .withMessage("New Password is required")
    .isLength({ min: 6 })
    .withMessage("Password should be at least 6 characters long"),
  check("confirmedPassword").custom((value, { req }) => {
    if (value !== req.body.newPassword) {
      throw new Error("Passwords do not match");
    }
    return true;
  }),
];

const { check } = require("express-validator");

const validateProduct = [
  check("name")
    .trim()
    .notEmpty()
    .withMessage("Product Name is required")
    .isLength({ min: 3, max: 200 })
    .withMessage("Product Name should be at least 3-200 characters long"),
  check("description")
    .trim()
    .notEmpty()
    .withMessage("Description is required")
    .isLength({ min: 3 })
    .withMessage("Description should be at least 3 characters long"),
  check("price")
    .trim()
    .notEmpty()
    .withMessage("Price is required")
    .isFloat({ min: 0 })
    .withMessage("Price must be a positive number"),
  check("category").trim().notEmpty().withMessage("Category is required"),
  check("quantity")
    .trim()
    .notEmpty()
    .withMessage("Quantity is required")
    .isInt({ min: 1 })
    .withMessage("Quantity must be a positive integer"),
];

module.exports = { validateProduct };
```

- step 3: run the validation

```js
// validation/index.js
const { check, validationResult } = require("express-validator");

exports.runValidation = (req, res, next) => {
  const errors = validationResult(req);
  if (!errors.isEmpty()) {
    let errorsList = errors.array().map((error) => error.msg);
    // return res.status(400).json({ errors: errorsList });
    return res.status(422).send({
      success: false,
      message: errors.array()[0].msg,
    });
  }

  next();

  // method2
  // const errors = validationResult(req);
  // console.log(errors);
  // if (!errors.isEmpty()) {
  //   const validationErrors = {};
  //   const allErrors = errors.array();
  //   allErrors.forEach((error) => {
  //     validationErrors[error.param] = error.msg;
  //   });

  //   return res.status(400).json({
  //     validationErrors,
  //   });
  // }
  // return next();

  // method 3
  // const errors = validationResult(req);
  // if (!errors.isEmpty()) {
  //   return res.status(422).json({
  //     error: errors.array()[0].msg,
  //   });
  // }
  // return next();
};
```

## Follow Me

[<img src='https://cdn.jsdelivr.net/npm/simple-icons@3.0.1/icons/github.svg' alt='github' height='40'>](https://github.com/learnwithfair) [<img src='https://cdn.jsdelivr.net/npm/simple-icons@3.0.1/icons/facebook.svg' alt='facebook' height='40'>](https://www.facebook.com/learnwithfair/) [<img src='https://cdn.jsdelivr.net/npm/simple-icons@3.0.1/icons/instagram.svg' alt='instagram' height='40'>](https://www.instagram.com/learnwithfair/) [<img src='https://cdn.jsdelivr.net/npm/simple-icons@3.0.1/icons/twitter.svg' alt='twitter' height='40'>](https://www.twiter.com/learnwithfair/) [<img src='https://cdn.jsdelivr.net/npm/simple-icons@3.0.1/icons/youtube.svg' alt='YouTube' height='40'>](https://www.youtube.com/@learnwithfair)

<!-- MARKDOWN LINKS & IMAGES -->

[youtube-shield]: https://img.shields.io/badge/-Youtube-black.svg?style=flat-square&logo=youtube&color=555&logoColor=white
[youtube-url]: https://youtube.com/@learnwithfair
[facebook-shield]: https://img.shields.io/badge/-Facebook-black.svg?style=flat-square&logo=facebook&color=555&logoColor=white
[facebook-url]: https://facebook.com/learnwithfair
[instagram-shield]: https://img.shields.io/badge/-Instagram-black.svg?style=flat-square&logo=instagram&color=555&logoColor=white
[instagram-url]: https://instagram.com/learnwithfair
[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=flat-square&logo=linkedin&colorB=555
[linkedin-url]: https://linkedin.com/company/learnwithfair
