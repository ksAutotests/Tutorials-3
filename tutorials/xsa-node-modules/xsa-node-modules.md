---
title: Modules and Express
description: Working with Node.js modules
tags: [  tutorial>intermediate, products>sap-hana, products>sap-hana\,-express-edition ]
---
## Prerequisites  
 - **Proficiency:** Intermediate
 - **Tutorials:** [SAP HANA XS Advanced, Creating a Node.js Module](http://go.sap.com/developer/tutorials/xsa-xsjs-xsodata.html)

## Next Steps
 - [HANA Database Access from Node.js](http://go.sap.com/developer/tutorials/xsa-node-dbaccess.html)

## Details
### You will learn  
In a previous tutorial you created a [SAP HANA XS Advanced, Creating a Node.js Module](http://go.sap.com/developer/tutorials/xsa-xsjs-xsodata.html), but didn’t really do much Node.js specific programming.  You were only using Node.js to run XSJS and XSODATA services. The support for XSJS and XSODATA is an important feature for XS Advanced. It not only allows backward compatible support for much of your existing development; but it provides a simplified programming model as an alternative to the non-block I/O event driven programming model normally used by Node.js

### Time to Complete
**15 Min**.

---

1. Return to the Node.js module and the `server.js` source file. You currently have enough Node.js logic to start up the XSJS compatibility and that’s it. You would like to extend `server.js` to also handle some purely Node.js code as well. At the same time we still want to support our existing XSJS and XSODATA services from this `server.js`.  

	![server file](1.png)

2. Begin by adding two new Node.js module requirements toward the beginning of the file.  One is for the http built-in module and the other is the popular open source module – express. One of the most common tasks in Node.js is acting as a web server and handling `http requests/responses`. express is a module that wraps and extends the low level http library and provides many additional services. 

	```
	/*eslint no-console: 0, no-unused-vars: 0*/
	```

3. You still want to configure the XSJS module but no longer want it to listen directly on your service port. Instead you will start your own instance of express add a route handler for `/node` which you can code your own Node.js logic. Then you will add the XSJS as a root route handler. Here is the complete new coding of your `server.js`. 

	```
	*eslint no-console: 0, no-unused-vars: 0*/
	```

4. Notice that in the previous additions to `server.js` you added a reference to a module called `./myNode`. This is a Node.js module which will be local to your project. Modules don’t all have to come from central repositories. They can also be a way of modularizing your own code (similar to XSJSLIB files). That is exactly what you will do here. Rather than filling up your `server.js` with application specific logic, you will break that out into its own Node.js module named `myNode.js`. 

	![reference](4.png)

5. Create a new file in your `js` folder called `myNode.js`

	![new file](5.png)

6. Add the following code to your `myNode.js` file. This will add a simple GET handler that returns a “Hello World” message when requested. Notice express in this module has a root route handler. But this will relatively to where it is attached in `server.js`.  Therefore this logic will still respond relative to the `/node` route handler base we specified earlier. 

	```
	"use strict";
	```

7. Look at the `package.json` file in the editor. You will see the dependencies section which lists all required libraries and their versions. You manually added the express Node.js module to your project, so you also need to extend the dependencies section here. 

	![package](7.png)

8. Your Node.js module is essentially finished, however before you can run it you also need to add a new route to the `xs-app.json` of your `HTML5` module.  

	```
	{
	```

9. You can now run the `js` module.

	![run the module](9.png)

10. You should see that the build and deploy was successful. 

	![successful build](10.png)

11. However if you go to the tab where the service run was started, you will see an Unauthorized message just as you did in [SAP HANA XS Advanced, Creating a Node.js Module](http://go.sap.com/developer/tutorials/xsa-xsjs-xsodata.html).  This is as intended.

	![unauthorized](11.png)

12. So now run the `web` module. It will need to rebuild and redeploy due to the added route.

	![run the module](9.png)

13. In the running tab, you should see the `index.html` from earlier. You can add the URL to your XSJS service `/index.xsjs` in the browser. This will test to make sure that your XSJS and XSODATA paths are still accessible even though you swapped out the root handler.

	![running tab](9.png)

14. Now change the path in the browser to `/node/`.  You should see "Hello World" Node.js this is being returned from the new route handler and Node.js module you just implemented in this exercise. 


## Next Steps
 - [HANA Database Access from Node.js](http://go.sap.com/developer/tutorials/xsa-node-dbaccess.html)