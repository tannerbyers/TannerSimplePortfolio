---
title: "On My Way App"
date: 2020-03-17T21:22:25-04:00
draft: false
---


# **[OMW APP](https://omwapppipeline.herokuapp.com/)**

OMW APP is a one page web app for texting saved contacts with as few clicks as possible. Created using simple HTML, JS, and Bootstrap.

In building this project, I learned how to read API Documentation to use 3rd Party API's and how to save,get, and delete data from Localstorage.

This is where the Texting "magic" happens. I am using the textbelt api to send the requested message to the list number: 
{{< highlight Javascript "linenos=false" >}}
  request.post('https://textbelt.com/text', {
        form: {
            phone: (req.body.toPhoneNumber),
            message: (req.body.textMessage),
            key: 'textbelt',
        },
    }, function(err, httpResponse, body) {
        if (err) {
            console.error('Error:', err);
            return;
        }

        APIResponse = JSON.parse(body);
        console.log(APIResponse.success);

        if (APIResponse.success) {
            res.send(req.body.textMessage);
        } else {
            res.send(APIResponse.error)
        }

    })
{{< / highlight >}}
