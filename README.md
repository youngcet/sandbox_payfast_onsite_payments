<p align="center">   
    <a href="https://pub.dev/packages/payfast"><img src="https://img.shields.io/pub/v/payfast?logo=dart&logoColor=white" alt="Pub Version"></a>
    <a href="https://pub.dev/packages/payfast"><img src="https://badgen.net/pub/points/payfast" alt="Pub points"></a>
    <a href="https://pub.dev/packages/payfast"><img src="https://badgen.net/pub/likes/payfast" alt="Pub Likes"></a>
    <a href="https://pub.dev/packages/payfast"><img src="https://badgen.net/pub/popularity/payfast" alt="Pub popularity"></a>
    <br> 
    <a href="https://github.com/youngcet/payfast"><img src="https://img.shields.io/github/stars/youngcet/payfast?style=social" alt="Repo stars"></a>
    <a href="https://github.com/youngcet/payfast/commits/main"><img src="https://img.shields.io/github/last-commit/youngcet/payfast/main?logo=git" alt="Last Commit"></a>
    <a href="https://github.com/youngcet/payfast/pulls"><img src="https://img.shields.io/github/issues-pr/youngcet/payfast" alt="Repo PRs"></a>
    <a href="https://github.com/youngcet/payfast/issues?q=is%3Aissue+is%3Aopen"><img src="https://img.shields.io/github/issues/youngcet/payfast" alt="Repo issues"></a>
    <a href="https://github.com/youngcet/payfast/graphs/contributors"><img src="https://badgen.net/github/contributors/youngcet/payfast" alt="Contributors"></a>
    <a href="https://github.com/youngcet/payfast/blob/main/LICENSE"><img src="https://badgen.net/github/license/youngcet/payfast" alt="License"></a>
    <br>       
    <a href="https://app.codecov.io/gh/youngcet/payfast"><img src="https://img.shields.io/codecov/c/github/youngcet/payfast?logo=codecov&logoColor=white" alt="Coverage Status"></a>
</p>

## PayFast Onsite Payment Integration Sandbox Example

The following HTML code demonstrates how to integrate with the PayFast Onsite Payment Engine. This file is crucial for handling onsite payments within your application. **Do not modify the code below the specified comment.**

### Example Code

```html
<html>
<head>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <script src="https://sandbox.payfast.co.za/onsite/engine.js"></script>
</head>
<body>
    <script>
        // DO NOT MODIFY THE CODE BELOW
        
        // Retrieve the UUID from the URL query string
        const queryString = window.location.search;
        const urlParams = new URLSearchParams(queryString);
        const uuid = urlParams.get('uuid');
        
        // Pass the UUID to the PayFast Onsite Payment Engine
        window.payfast_do_onsite_payment({"uuid":uuid}, function (result) {
            if (result === true) {
                // Payment successfully completed
                location.href = 'completed'; // Redirects to trigger the payment completed widget in the app
            } else {
                // Payment window closed by the user
                location.href = 'closed'; // Redirects to trigger the payment cancelled widget in the app
            }
        }); 
    </script>
</body>
</html>
```

### Adding support for Payfast's Web package
To support the [Payfast's Web package](https://github.com/youngcet/payfast_web), you can amend the file as shown below:
```html
<html>
<head>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <script src="https://sandbox.payfast.co.za/onsite/engine.js"></script>
</head>
<body>
    <script>
        // DO NOT MODIFY THE CODE BELOW
        
        // Retrieve the UUID from the URL query string
        const queryString = window.location.search;
        const urlParams = new URLSearchParams(queryString);
        const uuid = urlParams.get('uuid');
        const return_url = urlParams.get('return_url'); // -> add to support web
        const cancel_url = urlParams.get('cancel_url'); // -> add to support web

        window.payfast_do_onsite_payment({"uuid":uuid}, function (result) {
            if (result === true) {
                // Payment Completed
                location.href = decodeURIComponent(return_url) || 'completed'; // triggers payment completed widget on app
            }
            else {
                // Payment Window Closed
                location.href = decodeURIComponent(cancel_url) || 'closed'; // triggers payment cancelled widget on app
            }
        });
    </script>
</body>
</html>
```
