# Lab04 - Using the Admin API

Go to the Service credentials page and View credentials. To access the Kafka Admin API, use the value for property kafka_admin_url. The Swagger 2.0 docs for the IBM Event Streams Administration REST API is found at https://raw.githubusercontent.com/ibm-messaging/event-streams-docs/master/admin-rest-api/admin-rest-api.yaml. You can load the file via URL import in the http://editor.swagger.io, click File > Import URL > OK. Or read the README for the Admin API at https://github.com/ibm-messaging/event-streams-docs/tree/master/admin-rest-api.

To authenticate add an X-Auth-Token HTTP Header with the apikey found in the service credentials.

To use the Admin API you need the full `kafka_admin_url` and the `apikey` from the `Service Credentials`. In the examples below, replace the placeholders for these properties with the values from the `Service Credentials` of your Event Streams service,

* List the Kafka topics,
  
	```console
	$ curl -X GET \
	https://<kafka_admin_url>/admin/topics \
	-H 'X-Auth-Token: <apikey>'
	[
		{
			"name": "greetings",
			"partitions": 1,
			"replicationFactor": 3,
			"retentionMs": 86400000,
			"cleanupPolicy": "delete",
			"configs": {
				"cleanup.policy": "delete",
				"min.insync.replicas": "2",
				"retention.bytes": "104857600",
				"retention.ms": "86400000",
				"segment.bytes": "536870912"
			},
			"replicaAssignments": [
				{
					"id": 0,
					"brokers": {
						"replicas": [
							0,
							1,
							2
						]
					}
				}
			]
		}
	]
	```

* Delete a topic,
  
	```console
	$ curl -X DELETE \
	https://<kafka_admin_url>/admin/topics/greetings \
	-H 'X-Auth-Token: <apikey>'
	Create a topic,
	$ curl -X POST \
	https://<kafka_admin_url>/admin/topics \
	-H 'X-Auth-Token: <apikey>' \
	-d '{
	"name": "greetings",
	"partitions": 1
	}'
	```

* Get a topic,

	```console
	$ curl -X GET \
	https://<kafka_admin_url>/admin/topics/greetings \
	-H 'X-Auth-Token: <apikey>'
	```

* Update a topic configuration,

	```console
	$ curl -X PATCH \
	https://<kafka_admin_url>/admin/topics/greetings \
	-H 'X-Auth-Token: <apikey>' \
	-d '{
	"new_total_partition_count": 1
	}'
	```