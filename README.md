Facebook and Google Authentication Demo App

This repository contains a demo application built using .NET 5 that demonstrates how to implement Facebook and Google Authentication for logging into an application. The code and logic provided in this app are for educational purposes and can be used as a reference for integrating Facebook and Google Authentication in your .NET applications.

Features

	• Facebook and Google login integration.
	• Basic setup for OAuth authentication.
	• Demonstrates the use of middleware and configuration settings.
	• Clean and modular structure for easy understanding and customization.

Prerequisites

	• .NET 5 SDK installed.
	• A Facebook Developer account.
	• A Google Developer account.
	• Registered Facebook and Google Apps to obtain App ID, App Secret, Client ID, and Client Secret.

Setting Up the Facebook App

	1. Log in to Facebook for Developers.
	2. Create a new app: 
		○ Navigate to My Apps > Create App.
		○ Select "Consumer" as the app type and follow the instructions.
	3. Add Facebook Login to your app: 
		○ Navigate to Add a Product > Facebook Login.
		○ Select "Web" and specify your application's URL.
	4. Obtain the App ID and App Secret: 
		○ Navigate to Settings > Basic.
		○ Note down the App ID and App Secret.

Setting Up the Google App

	1. Log in to Google Cloud Console.
	2. Create a new project.
	3. Configure the OAuth consent screen: 
		○ Navigate to APIs & Services > OAuth consent screen.
		○ Fill in the required details.
	4. Create credentials: 
		○ Navigate to APIs & Services > Credentials.
		○ Click Create Credentials > OAuth 2.0 Client IDs.
		○ Choose "Web application" and specify the redirect URI (e.g., https://localhost:5001/signin-google).
	5. Obtain the Client ID and Client Secret.

Configuration

	1. Clone this repository:
		git clone https://github.com/rajibmahata/FacebookAuthentication.git
		cd FacebookGoogleAuthenticationDemo
	2. Update appsettings.json:
		{
		    "Authentication": {
		        "Facebook": {
		            "AppId": "YOUR_APP_ID",
		            "AppSecret": "YOUR_APP_SECRET"
		        },
		        "Google": {
		            "ClientId": "YOUR_CLIENT_ID",
		            "ClientSecret": "YOUR_CLIENT_SECRET"
		        }
		    }
		}
	3. Restore dependencies:
		dotnet restore
	4. Run the application:
		dotnet run
	5. Open your browser and navigate to https://localhost:5001. You should see a login page with options to log in via Facebook and Google.

How It Works

	1. Middleware Integration:
		○ The app uses the Microsoft.AspNetCore.Authentication.Facebook and Microsoft.AspNetCore.Authentication.Google packages to integrate authentication.
	2. Startup Configuration:
		○ In Startup.cs, the FacebookDefaults.AuthenticationScheme and GoogleDefaults.AuthenticationScheme are added to the authentication middleware.
	3. OAuth Flow:
		○ When a user clicks the "Login with Facebook" or "Login with Google" button, they are redirected to the respective provider for authentication.
		○ Upon successful login, the provider redirects back to the app with an authentication token.
	4. User Claims:
		○ The user's information (e.g., name, email) is retrieved from the provider and added to the authentication claims.

Code Highlights

	Authentication Configuration in Startup.cs:
 
		services.AddAuthentication(options =>
		{
		    options.DefaultAuthenticateScheme = CookieAuthenticationDefaults.AuthenticationScheme;
		    options.DefaultChallengeScheme = FacebookDefaults.AuthenticationScheme;
		})
		.AddCookie()
		.AddFacebook(options =>
		{
		    options.AppId = Configuration["Authentication:Facebook:AppId"];
		    options.AppSecret = Configuration["Authentication:Facebook:AppSecret"];
		})
		.AddGoogle(options =>
		{
		    options.ClientId = Configuration["Authentication:Google:ClientId"];
		    options.ClientSecret = Configuration["Authentication:Google:ClientSecret"];
		});
	
	Login and Logout: Routes to handle login and logout are implemented in AccountController.cs.

Limitations
	
	• This is a demo application and does not include advanced error handling or production-level security measures.
	• Only basic Facebook and Google Authentication are implemented; no additional API integrations are included.

Contributing

Contributions are welcome! Feel free to submit a pull request or open an issue if you have suggestions for improvements.

License

This project is licensed under the MIT License. See the LICENSE file for details.

Acknowledgments

•	[Microsoft Docs: Facebook Authentication](https://learn.microsoft.com/en-us/aspnet/core/security/authentication/social/facebook-logins?view=aspnetcore-9.0)
•	[Microsoft Docs: Google Authentication](https://learn.microsoft.com/en-us/aspnet/core/security/authentication/social/google-logins?view=aspnetcore-9.0)
•	[Facebook for Developers](https://developers.facebook.com/)
•	[Google Cloud Console](https://console.cloud.google.com/)


 
