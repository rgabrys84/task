SignupPage
class SignupPage extends Page
{
    static url = "https://panel.kontakt.io/signin"
    static at = { title == "Login to Kontakt.io Panel" }
    static content = {
        heading { $("h1").text() }
        errorHeading { $(".alert-error h4").text() }
        signupForm { $("form[id=signupForm]") }
        emailField { $("input[name=E-MAIL*]") }
        passwordField { $("input[name=PASSWORD*]") }
        submitButton(to: SignupResultPage) { $("button[type=signin]") }
    }
}


SignupPageIT.groovy
@Stepwise
class SignupPageIT extends GebReportingSpec {
 
    def "Signup Test Happy Path"() {
 
        given: "I'm at the sign up form"
        to SignupPage
 
        when: "I signup as a valid user"
        emailField = "rgabrys84@gmail.com"
         passwordField = "password"
        submitButton.click()
 
        then: "I'm at the result page "
        at SignupResultPage
 
    }
}



SignupPageIT.groovy
class SignupPageIT extends GebReportingSpec {
 
    def "Signup Test for Invalid User"() {
 
        given: "I'm at the sign up form"
        to SignupPage
 
        when: "I signup as an invalid user"
        emailField = "rgab@gmail.com"
        passwordField = "password"
        submitButton.click(SignupPage)
 
        then: "I'm at the sign up page again "
        at SignupPage
        errorHeading == "Error!"
    }
}
