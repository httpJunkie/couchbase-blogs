# Couchbase SDK Playground

We have launched a new project now available at [Couchbase.live](https://couchbase.live), which helps new developers learning Couchbase to explore the different SDKs for Java, NodeJS, .NET, and Python. You can currently try out code that utilizes the individual SDKs. This blog post will take you on a brief tour and get you running code against a live Couchbase Server container.

We have built this technology in the Go programming language on top of AWS so that you can very quickly spin up a Couchbase Server container and Web UI and run code against our sample datasets.

## An Introduction

You can get started by browsing to [Couchbase.live](https://couchbase.live). If you try to run code immediately without starting a test-drive, your data will not be persisted from one execution to the next, so I suggest logging into Couchbase Live using the Start-Test Drive button. 

![](images/start-session.png)

Once you select to start a test drive, complete the basic form and login. This gives you access to a Couchbase Server instance where you can run code in your preferred language persisting any data changes from one execution to the next.

![](images/session-info.png)

Upon logging in, you will see information at the top of the screen specific to your current Couchbase Server instance. Let's use this information to log into the Web Admin.

> Note: This test-drive session is active until there's ~10 min of inactivity.

If you click on the Web Admin UI link, you will be prompted to enter a username and password, which you can find in **Your Couchbase Instance**. These fields are underlined in the screenshot above.

Just copy the information over to the login screen and you will be redirected to the Couchbase Server Dashboard where you will see two sample buckets installed: `beer-sample` and `travel-sample`.

![](images/buckets-view.png)

Available to you are the following services: **Query**, **Indexes**, **Search**, and **Views**. There are two services that will not be activated as well but do show up in the navigation, at this time **Analytics**, and **Eventing** are not available.

Our prebuilt examples on Couchbase.live are based on the `travel-sample` data set, however; you can alter the code or create your own data set to run code against on the bucket tab in the Web UI by clicking on **Add Bucket** in the top right-hand side of the screen. For the purposes of this blog post we will use the `travel-sample` dataset.

## Trying out the NodeJS Examples

After starting your session, click on the NodeJS **KV Get** example.

![](images/node-kv-get.png)

When you hit the You will get a response in the Output panel on the right side of the screen. This example will generate the following in the Output Panel:

    Result: 
    {
      cas: CbCas { '0': <Buffer 00 00 8b d7 55 19 48 16> },
      content: {
        callsign: 'MILE-AIR',
        country: 'United States',
        iata: 'Q5',
        icao: 'MLA',
        id: 10,
        name: '40-Mile Air',
        type: 'airline'
      }
    }

This code has retrieved one document with the key value of `airline_10`, but if you change the key on line 20 to `airline_112`, you will see that we get a new result in the Output Panel:

    Result: 
    {
      cas: CbCas { '0': <Buffer 00 00 94 d8 55 19 48 16> },
      content: {
        callsign: 'FLYSTAR',
        country: 'United Kingdom',
        iata: '5W',
        icao: 'AEU',
        id: 112,
        name: 'Astraeus',
        type: 'airline'
      }
    }

So we can update any of the examples with whatever code we want. This creates a nice little playground to test out samples from our documentation or just letting you explore by trying out some of our basic operations. 