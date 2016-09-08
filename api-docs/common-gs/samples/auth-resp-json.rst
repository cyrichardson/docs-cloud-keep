.. _auth-response-example:

.. code::

	{
		"access": {
			"token": {
				"id": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
				"expires": "2014-11-24T22:05:39.115Z",
				"tenant": {
					"id": "110011",
					"name": "110011"
				},
				"RAX-AUTH:authenticatedBy": [
					"APIKEY"
				]
			 },
			"serviceCatalog": [
				{
					"name": "cloudKeep",
					"endpoints": [
						{
							"publicURL":"https://iad.keep.rackspacecloud.com/v1.0/123456”,
							"region":"IAD",
							"tenantId":"123456",
						},
						{
							"publicURL":"https://ord.keep.rackspacecloud.com/v1.0/123456”,
							"region":"ORD",
							"tenantId":"123456",
						},
						{
							"publicURL":"https://lon.keep.api.rackspacecloud.com/v1.0/123456",
							"region":"LON",
							"tenantId":"123456",
						}
					],
					"type": "rax:keep"
				},
				{
					"name": "cloudDNS",
					"endpoints": [
						{
							"publicURL": "https://dns.api.rackspacecloud.com/v1.0/110011",
							"tenantId": "110011"
						}
					],
					"type": "rax:dns"
				},
				{
					"name": "rackCDN",
					"endpoints": [
						{
							"internalURL": "https://global.cdn.api.rackspacecloud.com/v1.0/110011",
							"publicURL": "https://global.cdn.api.rackspacecloud.com/v1.0/110011",
							"tenantId": "110011"
						}
					],

					"type": "rax:cdn"
				}
			],
			"user": {
				"id": "123456",
				"roles": [
					{
						"description": "A Role that allows a user access to keystone Service methods",
						"id": "6",
						"name": "compute:default",
						"tenantId": "110011"
					},
					{
						"description": "User Admin Role.",
						"id": "3",
						"name": "identity:user-admin"
					}
				],
				"name": "jsmith",
				"RAX-AUTH:defaultRegion": "ORD"
			}
		}
	}
