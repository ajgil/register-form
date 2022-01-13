step 1 rellenar el formulario enviarlos al backend mediante función async

step 2 Recibe sms, valida el token mediante función async

step 3 Gracias y volver a home

Estas son las funciones async al backend que deben ser llamadas en los steps

```
async function getToken() {
    const name = odenameRef.current.value
	const email = odeemailRef.current.value
	const pass = odepasswordRef.current.value
	const pass2 = odePasswordConfirmRef.current.value
    const phone = odephone

	if (pass !== pass2) {
        alert("Passwords don't match");
		return
    }
	if (phone) {
	const { error } = await supabase.auth.signUp({
		email: email,
        password: pass, 
        },{
        data:{
            ode: true,
            firstname: name,
            phone: phone,
        }
        })
        if (error) {
            console.log(error)
            alert('error en el registro con email')
        }
    const { errorPhone } = await supabase.auth.signUp({
        phone: phone,
        password: pass,
        },{
            data: {
                ode: true,
                firstname: name,
                email: email,
            }
        })
        if (errorPhone) {
            console.log(error)
            alert('error en el registro con teléfono')
    }
    }
		setOptShow(true) 
  }

async function verifyOTP() {
    console.log('dentro VerifyOTP')
    const phone = odephone
    const token = token

    console.log('verifyOTP', phone)
    console.log('verifyOTP', token)

    console.log('verify otp datos', phone, token)
    const { error } = await supabase.auth.verifyOTP({
        phone: phone,
        token: token, 
        },{
            data:{
                ode: true,
                verified: true,
            }
        })
        if (error) {
            console.log(error)
            alert('error al verificar el token OTP')
        }
}
```