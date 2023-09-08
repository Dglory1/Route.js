# Route.js
How to fix import in route.js etc
```

Documents\FULLSTACK-MERN-MOVIE-2022\server\src\routes\index.js
    at new NodeError (node:internal/errors:405:5)
    at finalizeResolution (node:internal/modules/esm/resolve:226:11)
    at moduleResolve (node:internal/modules/esm/resolve:838:10)
    at defaultResolve (node:internal/modules/esm/resolve:1036:11)
    at DefaultModuleLoader.resolve (node:internal/modules/esm/loader:251:12)
    at DefaultModuleLoader.getModuleJob (node:internal/modules/esm/loader:140:32)
    at ModuleWrap.<anonymous> (node:internal/modules/esm/module_job:76:33)
    at link (node:internal/modules/esm/module_job:75:36) {
  code: 'ERR_MODULE_NOT_FOUND'
}

Node.js v20.5.0
[nodemon] app crashed - waiting for file changes before starting...


```
2. user.route.js
   ```
import express from "express"; 
import userRoute from "./user . route. js";
import mediaRoute from "./media.route. js";
import personRoute from "./person.route. js";
import reviewRoute from "./review. route. js"; 
const router = express. Router( ); 
router .use("/user", userRoute);
router .use("/person", personRoute) ;

router .use("/reviews", reviewRoute);
2)user.route.js


Import express from "express" 
import [body) from"express-validator" 
import favoriteController from " .. /controllers/favorite. controller. js"
import userController from " .. /controllers/user. controller.js" 
import requestHandler from " .. /handlers/request. handler.js"
import userModel from " .. /models/user.model.js"

import tokenMiddleware from " .. /middlewares/token.middleware. js"
 const router = express.Router();

router .post ( 
    "/signup", 
    body ("username") 
        exists() .withMessage("username is required")

        .isLength([ min: 8 }) .withMessage("username minimum 8 characters")

        .custom(async value => { 
                 const user - await userModel.findone(( username: value });
                 if (user) return Promise.reject("username already used");
        });

    body("password")

        .exists/1.withMessage("password is required")
        .isLength({ min: 8 } ) .withMessage( "password minimum 8 characters"), 
    body ("confirmPassword")

        .exists().withMessage("confirmPassword is required")

        .isLength({ min: 8 }) .withMessage("confirmPassword minimum 8 characters")

       .custom((value, { req }) -> { 
              if (value ! == req.body .password) throw new Error("confirmPassword not match"); 
              return true;
       }),
 
    body("displayName")

        .exists() .withMessage("displayName is required")

        .isLength({ min: 8 }) .withMessage("displayName minimum 8 characters"), 
    requestHandler . validate,
    userController .signup
),

router .post (

     "/signin",
     body("username")
         .exists() .withMessage("username is required")

         .isLength({ min: 8 }) .withMessage("username minimum 8 characters"), 
     body ("password")

          .exists() .withMessage("password is required")

          .isLength({ min: 8 }) . withMessage("password minimum 8 characters"), 
      requestHandler .validate, 
      userController.signin
);
router.put(

     "/update-password",
     tokenMiddleware.auth,
     body("password")

          .exists() .withMessage("password is required")

          .isLength({ min: 8 }) . withMessage( "password minimum 8 characters"), 
     body( "newPassword")

          .exists() .withMessage("newPassword is required")

          .isLength({ min: 8 }) . withMessage("newPassword minimum 8 characters"),
     body("confirmNewPassword")

          .exists() .withMessage("confirmNewPassword is required")

          .isLength({ min: 8 }) . withMessage("confirmNewPassword minimum 8 characters")   
          .custom((value, { req }) => { 
                if (value ! == req. body . newPassword) throw new Error("confirmNewPassword not match"); 
                return true;
          }),
      requestHandler . validate, 
      userController .updatePassword
 ), 

router .get( 
      "/info",
      tokenMiddleware.auth, 
      userController .getInfo,
);

router .get (

      "/favorites",
      tokenMiddleware.auth,
      favoriteController.getFavoritesofUser
);
router . post ( 
      "/favorites", 
      tokenMiddleware.auth, 
      body("mediatype")
          .exists() .withMessage("mediatype is required")

          .custom(type => ["movie", "tv"].includes(type)) .withMessage("mediaType invalid"), 
      body("mediaId")

          .exists().withMessage("mediaId is required")

          .isLength(( min: 1 )) .withMessage("mediaId can not be empty"),
      body ( "mediaTitle")

         .exists().withMessage("mediaTitle is required"), 
      body ( "mediaPoster")
         .exists( ) .withMessage( "mediaPoster is required").
      body ( "mediaRate")
         .exists() .withMessage("mediaRate is required"), 
      favoriteController.addFavorite
);
router .delete(
      "/ favorites/ : favoriteId", 
      tokenMiddleware. auth, 
      favoriteController.removeFavorite
);

export default router;
```
