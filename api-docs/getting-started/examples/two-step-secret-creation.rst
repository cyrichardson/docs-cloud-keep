.. _gsg-two-step-secret-creation:


Create and store a secret by using two requests 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

When you cannot easily provide secret data inside the JSON data in the initial
POST request, you can use a subsequent PUT request to provide the data.


#. Create the secret metadata in Cloud Keep by sending a **POST** request as
   shown in the following example:

   .. code::

      $ curl -X POST -H 'Content-Type: application/json' \
             -H 'X-Auth-Token: '$AUTH_TOKEN' -d \
             {
               "name": "Binary Key File"
             }' $ENDPOINT/v1/secrets

   If the call is successful, you receive a ``201 Created`` response that
   includes the reference to the newly created secret as shown in the
   following example:

   .. code::

    {"secret_ref": "https://iad.keep.api.rackspacecloud.com/v1/secrets/943c8f98-e980-4cc4-0da1-8ed0993bcf55"}

   The secret metadata is now stored in Cloud Keep with a secret ID of
   ``943c8f98-e980-4cc4-0da1-8ed0993bcf55``. Note that you have only stored
   the metadata, not the actual secret data itself.  You need to remember the
   secret ID for the subsequent **PUT** request that will store the payload
   itself. You can export it to an environment variable, as follows.

   .. code::

      $ export SECRET_ID=943c8f98-e980-4cc4-0da1-8ed0993bcf55

#. Create a file with random data to be used as a secret key file.
   The following command creates a 5 KB file in
   the current directory that contains random data:

   .. code::

      $ dd if=/dev/random of=secret_key_file count=5 bs=1024

#. Submit a **PUT** request that includes the secret key file that you
   just created as shown in the following example:

   .. code::

      $ curl -i -X PUT -H "Content-Type: application/octet-stream" \
             -H "X-Auth-Token: $AUTH_TOKEN" \
             -T ./secret_key_file $ENDPOINT/v1/secrets/$SECRET_ID

   Cloud Keep encrypts and stores the contents of the secret key file,
   associates it with the previously created metadata, and responds with an
   empty ``204 No Content`` message, as shown in the following example:

   .. code::

        HTTP/1.1 204 No Content
        Date: Tue, 01 Mar 2016 23:13:10 GMT
        Via: 1.1 Repose (Repose/7.3.1.0)
        Date: Tue, 01 Mar 2016 23:13:10 GMT
        x-trans-id: ekdmc8F1ZXN0SWQiOiIzMTMyNTQ4ZS00NDA1LTQ2OTgtOTYzOS0093jcmksz5DA1ZTYiLCJvcmlnaW4iOm51bGx9
        X-NewRelic-App-Data: kjm83ghzn0oTVVBaBAYGXlwTGhE1AwE2QgNWEVlbQFtcCxY0QwgcFFUZRAQFEV1HQ0sCWlYIB15cVBtXUFFaTwRXCgQVWgdWAkhbB1QABFBdUwcEUFMaHwBIUUwFAQFRXAUGA1tfUFEEVQlUABQBAwFVFUMEBFBaVgMAWVBQDQQAVVJTFR1RBwhCU24=
        x-openstack-request-id: req-c90c5678-c3df-9279-a94c-94c9f5c062e3
        Server: Jetty(9.2.z-SNAPSHOT)

Now you can use a **GET** request to retrieve the secret, as explained
in :ref:`Retrieve a secret <gsg-retrieve-a-secret>`.
