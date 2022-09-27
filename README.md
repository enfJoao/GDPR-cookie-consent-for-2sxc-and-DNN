# GDPR-cookie-consent-for-2sxc-and-DNN
This is a very basic 2sxc app to be injected in the footer of your theme so that it loads the modals and bar for the cookie consent module.

How to setup:
- If you use the DNN module share functionallity, just add the app and share it. No aditional steps needed.
- If you use the 2sxc module injection into the theme, add these lines to your theme file where you need the module:


	<%@ Import Namespace="DotNetNuke.Entities.Modules" %>
	<%@ Import Namespace="ToSic.Sxc.Dnn" %>
	<%@ Import Namespace="ToSic.Sxc.Services" %>
	
	<%
		var moduleController = new ModuleController();
		ModuleInfo footerModule = moduleController.GetAllModules().Cast<ModuleInfo>().Where(m => m.ModuleTitle == "CookieModule").FirstOrDefault();
		if (footerModule != null) {
			var tabId = footerModule.TabID;
			var moduleId = footerModule.ModuleID;
	%>
			<%= this.GetScopedService<IRenderService>().Module(tabId, moduleId) %>
	<%
		}
	%>
  
  
  As any 2sxc app, you will need to setup your own stuff in three places:
  - The app data (two data types: CookieTypes and CookieItems). Types are the groups for the cookies. Items are each cookie setup individually. These are translatable.
  - The resources (translations for all the text in the module itself)
  - The settings (I put all the modal/bar/buttons here, along with all the classes that can be added to stuff)
  
  As far as I'm concerned, this will need Bootstrap and jquery.
  
  For custom cookies you want to enable or disable, you will need to create your own code to do so. For example tagmanager can by customized in google settings to load only after a cookie exists in your site. You can use the cookie create and remove functions from this app.
