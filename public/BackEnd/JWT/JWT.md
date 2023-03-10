## JWT - JsonWebToken

JsonWebToken nos ayudará a generar tokens para mantener la sesión del usuario en nuestro proyecto, así como su ID para poder pedir los datos en MongoDB. Para ello necesitamos que se cree un token cada vez que el usuario se registra o inicia sesión, por lo que será necesario utilizarlo en nuestro controller de las rutas de usuario.  
Cuando generamos el token necesitaremos una key secreta para encriptar los mismos, la misma debemos crearla en nuestro archivo `.env` y luego pedirla cuando la necesitemos. La misma quedará de la siguiente manera.

```env
JWT_SECRET=<la key que nosotros querramos usar>
```

Con la key declarada podemos empezar a desarrollar el código para crear el token en nuestro controlador, el cual quedaría de la siguiente manera.

```js
const bcrypt = require("bcrypt")
const userModel = require("../models/user")
const jwt = require("jsonwebtoken")         // Requerimos JWT 
const secret = process.env.JWT_SECRET       // Y guardamos nuestra key en una variable

module.exports = {

    // Create a new user on the database

    users_createNewUser: (req, res) => {
        try {
            const user = new userModel(req.body)
            user.save((err, userResult) => {
                if (err) {
                    return res.status(500).json({
                        message: "The email is already in use"
                    })
                }
                const token = jwt.sign({              // Creamos el token con el método sign
                    id: userResult._id                // Y le agregamos el user id al token
                }, secret, {                          // Le pasamos la secret key que creamos
                    expiresIn: 60 * 60 * 24 * 30      // Y le indicamos que expira en 30 días
                })
                res.status(200).json({                // Le indicamos un estado correcto al front
                    auth: true,                       // Indicamos que está autorizado
                    token                             // Y le enviamos le token con la información del usuario
                });
            })
        } catch (err) {
            console.log(err)
            res.status(409).send(err)
        }
    },


    //  Find a user on the database

    users_getUserFromDataBase: (req, res) => {
        try {
            userModel.findOne({
                email: req.query.email
            }, (err, user) => {
                if (err) return res.status(400).send({
                    message: err.message
                })
                bcrypt.compare(req.query.password, user.password, function (error, isMatch) {
                    if (error) {
                        throw error
                    } else if (!isMatch) {
                        res.status(500).send("Password doesn't match!")
                    } else {
                        res.status(200).send(user)
                    }
                })
            })
        } catch (err) {
            console.log(err)
            res.status(409).send(err)
        }
    },

    // Update a user on the database

    users_updateUserOnDatabase: (req, res) => {
        console.log(req.body)
        res.send("hi, put")
    },

    // Delete a user on the database

    users_deleteOneUserOnDatabase: (req, res) => {
        console.log(req.body)
        res.send("hi, delete")
    },
}
```
