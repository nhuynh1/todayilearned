# Reusing schemas in Yup

Date: Sep 3, 2020
Tags: React

## Instead of rewriting Yup schemas from scratch start with a base schema and extend it

Use the `object.shape()` to add fields to a Yup object. A schema is returned.

```jsx
import * as Yup from 'yup';

export const baseSchema = Yup.object({
    firstName: Yup.string().required("Required"),
    lastName: Yup.string().required("Required"),
    addressOne: Yup.string().required("Required"),
    addressTwo: Yup.string(),
    municipality: Yup.string().required("Required"),
    provinceTerritory: Yup.string().required("Required"),
    postalCode: Yup.string().trim()
        .required("Required")
        .matches(/^[A-Za-z]\d[A-Za-z][ -]?\d[A-Za-z]\d$/,
            { message: "Postal Code must be in format: K4B 1H9" })
});

const extendedSchema = baseSchema.shape({
        email: Yup.string().trim().required("Required").email(),
        shipping: Yup.string().required("Required")
    })
```

Yup is a schema validation package that works well with Formik—a React forms library

```bash
npm install --save yup
```

**References:**

- [yup documentation](https://github.com/jquense/yup#objectshapefields-object-nosortedges-arraystring-string-schema)
- [Formik documentation](https://formik.org/docs/overview#complementary-packages)