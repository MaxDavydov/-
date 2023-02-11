{
	"info": {
		"_postman_id": "1f8897e1-ad07-401a-80ac-0bfed16d5cc1",
		"name": "PetFriends",
		"schema": "https://schema.getpostman.com/json/collection/v2.1.0/collection.json",
		"_exporter_id": "24524827"
	},
	"item": [
		{
			"name": "api.key",
			"event": [
				{
					"listen": "test",
					"script": {
						"exec": [
							"pm.test(\"Status code is 200\", function () {\r",
							"    pm.response.to.have.status(200);\r",
							"});\r",
							"pm.test(\"Key in responseBody\", function () {\r",
							"    var jsonData = JSON.parse(responseBody);\r",
							"    pm.collectionVariables.set(\"auth_key\", jsonData.key);\r",
							"});"
						],
						"type": "text/javascript"
					}
				}
			],
			"request": {
				"method": "GET",
				"header": [
					{
						"key": "email",
						"value": "maksimdavydov29@gmail.com",
						"type": "text"
					},
					{
						"key": "password",
						"value": "951753852max",
						"type": "text"
					}
				],
				"url": {
					"raw": "{{base_url}}/api/key",
					"host": [
						"{{base_url}}"
					],
					"path": [
						"api",
						"key"
					]
				}
			},
			"response": []
		},
		{
			"name": "api.pets",
			"event": [
				{
					"listen": "test",
					"script": {
						"exec": [
							"pm.test(\"Status code is 200\", function () {\r",
							"    pm.response.to.have.status(200);\r",
							"    var jsonData = JSON.parse(responseBody);\r",
							"    pm.collectionVariables.set(\"petid\", jsonData.id);\r",
							"    var jsonData = JSON.parse(responseBody);\r",
							"    pm.collectionVariables.set(\"name\", jsonData.name);\r",
							"});"
						],
						"type": "text/javascript"
					}
				}
			],
			"request": {
				"method": "POST",
				"header": [],
				"body": {
					"mode": "formdata",
					"formdata": [
						{
							"key": "name",
							"value": "Baron",
							"type": "text"
						},
						{
							"key": "animal_type",
							"value": "French buldog",
							"type": "text"
						},
						{
							"key": "age",
							"value": "5",
							"type": "text"
						},
						{
							"key": "pet_photo",
							"type": "file",
							"src": "rJnMJyXGC/french-bulldog.jpg"
						}
					]
				},
				"url": {
					"raw": "{{base_url}}/api/pets",
					"host": [
						"{{base_url}}"
					],
					"path": [
						"api",
						"pets"
					],
					"query": [
						{
							"key": "email",
							"value": "maksimdavydov29@gmail.com",
							"disabled": true
						},
						{
							"key": "key",
							"value": "951753852max",
							"disabled": true
						}
					]
				}
			},
			"response": []
		},
		{
			"name": "api/pets/:pet_id",
			"event": [
				{
					"listen": "test",
					"script": {
						"exec": [
							"pm.test(\"Новое имя не равно старому имени\", function () {\r",
							"    var jsonData = JSON.parse(responseBody);\r",
							"    pm.expect(pm.collectionVariables.get(\"name\")).to.not.equal(jsonData.name);\r",
							"    var jsonData = JSON.parse(responseBody);\r",
							"    pm.collectionVariables.set(\"petid\", jsonData.id);\r",
							"    var jsonData = JSON.parse(responseBody);\r",
							"    pm.collectionVariables.set(\"name\", jsonData.name);\r",
							"   \r",
							"\r",
							"    \r",
							"});"
						],
						"type": "text/javascript"
					}
				}
			],
			"request": {
				"method": "PUT",
				"header": [],
				"body": {
					"mode": "formdata",
					"formdata": [
						{
							"key": "name",
							"value": "Deks",
							"type": "text"
						},
						{
							"key": "animal_type",
							"value": "{{animal_type}}",
							"type": "text",
							"disabled": true
						},
						{
							"key": "age",
							"value": "{{age}}",
							"type": "text",
							"disabled": true
						},
						{
							"key": "pet_photo",
							"type": "file",
							"src": [],
							"disabled": true
						}
					]
				},
				"url": {
					"raw": "{{base_url}}/api/pets/{{petid}}",
					"host": [
						"{{base_url}}"
					],
					"path": [
						"api",
						"pets",
						"{{petid}}"
					]
				}
			},
			"response": []
		},
		{
			"name": "filter=my_pets",
			"event": [
				{
					"listen": "test",
					"script": {
						"exec": [
							"pm.test(\"имя равно имени первому питомцу\", function () {\r",
							"    var jsonData = JSON.parse(responseBody);\r",
							"    pm.expect(pm.collectionVariables.get(\"petid\")).to.equal(jsonData.pets[0].id);\r",
							"   \r",
							"\r",
							"    \r",
							"});"
						],
						"type": "text/javascript"
					}
				}
			],
			"request": {
				"method": "GET",
				"header": [],
				"url": {
					"raw": "{{base_url}}/api/pets?filter=my_pets",
					"host": [
						"{{base_url}}"
					],
					"path": [
						"api",
						"pets"
					],
					"query": [
						{
							"key": "filter",
							"value": "my_pets"
						}
					]
				}
			},
			"response": []
		}
	],
	"auth": {
		"type": "apikey",
		"apikey": [
			{
				"key": "value",
				"value": "38ba289bae36e678b8d8e239efa621bbf2504c74fa27033ad8c580af",
				"type": "string"
			},
			{
				"key": "in",
				"value": "header",
				"type": "string"
			},
			{
				"key": "key",
				"value": "auth_key",
				"type": "string"
			}
		]
	},
	"event": [
		{
			"listen": "prerequest",
			"script": {
				"type": "text/javascript",
				"exec": [
					""
				]
			}
		},
		{
			"listen": "test",
			"script": {
				"type": "text/javascript",
				"exec": [
					""
				]
			}
		}
	],
	"variable": [
		{
			"key": "base_url",
			"value": "https://petfriends.skillfactory.ru",
			"type": "string"
		},
		{
			"key": "auth_key",
			"value": ""
		},
		{
			"key": "petid",
			"value": ""
		},
		{
			"key": "name",
			"value": ""
		},
		{
			"key": "animal_type",
			"value": "French buldog",
			"type": "string"
		},
		{
			"key": "age",
			"value": "5",
			"type": "string"
		}
	]
}
