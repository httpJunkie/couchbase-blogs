# Couchbase SDK Playground

We have launched a new project now available at [Couchbase.live](https://couchbase.live), helping developers learning Couchbase to explore the different SDKs for Java, NodeJS, .NET, and Python. You can currently try out code that utilizes the individual SDKs. This blog post will take you on a brief tour and get you running code against a live Couchbase Server container.

We have built this technology in the Go programming language on top of AWS, it's quick to spin up a Couchbase Server container complete with Web UI and start running code against our `travel-sample` dataset.

## Test-Drive

You can get started by browsing to [Couchbase.live](https://couchbase.live). If you try to run code immediately without starting a test-drive, your data will not be persisted from one execution to the next, so I suggest logging into Couchbase Live using the Start-Test Drive button.

![](images/start-session.png)

Once you select to start a test drive, you can login with a username and password. This gives you access to a Couchbase Server instance, code can be run in several of the preferred SDKs. Like earlier stated, a test-drive will ensure that data is persisted from one execution to the next.

![](images/session-info.png)

## An Quick Tour around the UI

Upon logging in, you will see info at the top of the screen specific to your current Couchbase Server instance. Let's use this information to log into the Web Admin.

> Note: This test-drive session is active until there's ~10 min of inactivity. If you do get logged out, you will be prompted to start a new test-drive and you can log right back in. Data will be lost from the last session.

If you click on the Web Admin UI link, you will be prompted to enter a username and password, **Your Couchbase Instance** will show the hashed values needed t o login (underlined in the screenshot above). These unique values will change from one test-drive to the nest.

Just copy the information over to the login screen and you will be redirected to the Couchbase Server Dashboard where you will see two sample buckets installed: `beer-sample` and `travel-sample`.

![](images/buckets-view.png)

Available to you are the following services: **Query**, **Indexes**, **Search**, and **Views**. TAt this time **Analytics**, and **Eventing** are not available, but may be included in future versions of the tool.

Our prebuilt examples in the left-side navigation use the `travel-sample` data set, however; you can alter the code or create your own data set to run code against on the bucket tab in the Web UI by clicking on **Add Bucket**. For the purposes of this blog post we will use the `travel-sample` dataset as the code is already set up to use it and each session is only ten minutes. There are currently no options for saving your data or examples, so it's merely a playground to experiment with. Given more interest in the project this could be a feature we add.

## Trying out the NodeJS Examples

Let's walk ghrough some examples and see what eactly we can do. After starting your session, click on the NodeJS **KV Get** example.

![](images/node-kv-get.png)

When you hit the **Run** button, a response will show up in the **Output** panel on the right side of the screen. This example will generate the following in the Output Panel:

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

As we can see, we have retrieved one document with the key of `airline_10`, notice that if you change the key on line 20 to something else like: `airline_112` and **Run** again, a new result will show in the **Output**:

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

So we can update any of the examples with whatever code we want. This creates a nice playground expereince to test out samples from our documentation and each SDK language will have the same example titles so that it is easy to see what the code looks like for each operation in one SDK compared to another.

## Examples Featuring N1QL

I love being able to just play around with N1QL and test my knowledge of the query language, if you select one of the **Query** examples like **Query Rows**, we can test out a N1QL query and explore the possibilities. Let's choose that example, **Run** it, and then update the N1QL statement to:

```SQL
SELECT RAW r.author
FROM \`travel-sample\` t
UNNEST reviews AS r
WHERE t.type = "hotel"
  AND r.ratings.Overall > 3 LIMIT 5;
```

From looking at the data in the Web UI, one can see that a hotel document had a nested array of reviews. Understanding how the **UNNEST** clause works, I can test out an idea around selecting an author's name for reviews of hotels where the **Overall** rating is greater than 4 (top reviews).

