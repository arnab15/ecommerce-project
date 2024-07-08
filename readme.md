
# Web Services

Code based contains two Services main service and order service
- main Service : It contains Auth,Product and Order related Routes
- Order Service: It's a Kafka consumer based service which built for processing orders

## Github Links
- [Ecommerce Assignment ](https://github.com/arnab15/ecommerce-projec)
- [Main Service ](https://github.com/arnab15/main-service)
- [Order Service ](https://github.com/arnab15/order-service)


## How To run project?

- Make Sure You Have Docker and Docker compose installed in your local machine.
- Make Sure You have git installed in your local machine

Step 1 :  
```bash
  git clone https://github.com/arnab15/gamemano-assignment.git
```
Step 2 :  
```bash
  cd gamemano-assignment
```
Step 3 :  
```bash
  git submodule update --init --recursive
```
Step 4 :  
Create a .env file and add these environment variables or you can use env.example for reference.
```bash
ACCESS_TOKEN_SECRET=njvfdjdv9348vnu3u9b3urbu439
MONGO_DB_URL=mongodb://localhost:27017/game-ecommerce
NODE_ENV=production
KAFKA_URL=192.168.1.2:9092
```
Step 5 :  
```bash
  docker-compose up -d --build
```
Step 6 Seed DB:  
```bash
  docker exec -it main-service sh -c "npm run seed"
```
    
## How To run test?

- Make Sure Kafka and Zookeeper is running as containers
- Go to both order-service and main service and install dependencies using npm install commands

Then Go to Main Service and run  :  
```bash
  npm run test
```
## API Reference

#### Register

```http
  POST /api/register
```
### Request Body

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `name` | `string` | **Required** |
| `email` | `string` | **Required** |
| `password` | `string` | **Required** |

#### Login

```http
  POST /api/login
```
### Request Body

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `email` | `string` | **Required** |
| `password` | `string` | **Required** |

#### Get User profile details (Authentication Required)
make sure to pass Auth token in authorisation header

```http
  GET /api/profile
```

| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `id`      | `string` | **Required**. Id of item to fetch |


#### Update User role (Authentication Required & User must be Admin)

- make sure to pass Auth token in authorisation header

```http
  PUT /api/profile/:id/role
```

#### Request Params 
| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `id`      | `string` | **Required**. Id of user to update  |

#### Request Body 
| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `role`      | `string` | **Required**. (admin/user) |


## Product Routes

#### Add product (Authentication required & User Should be Admin)

```http
  POST /api/products
```
### Request Body

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `name` | `string` | **Required** |
| `description` | `string` | **Required** |
| `price` | `number` | **Required** |
| `category` | `string` | **Required** |

#### Update product (Authentication required & User Should be Admin)

```http
  PUT /api/products/:id
```
#### Request Params 
| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `id`      | `string` | **Required**. Id of product to update  |

### Request Body

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `name` | `string` | **Required** |
| `description` | `string` | **Required** |
| `price` | `number` | **Required** |
| `category` | `string` | **Required** |

#### Delete product (Authentication required & User Should be Admin)

```http
  DELETE /api/products/:id
```
#### Request Params 
| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `id`      | `string` | **Required**. Id of product to Delete  |

#### Get product Details

```http
  GET /api/products/:id
```
#### Request Params 
| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `id`      | `string` | **Required**. Id of product to Get details  |

#### Get products

```http
  GET /api/products?page=1&limit=10
```
#### Request Query Params 
| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `page`      | `number` | **Required**. current page number  |
| `limit`      | `number` | **Required**. no of record to fetch  |


## Order Routes

#### Place Order (Authentication required)

```http
  POST /api/orders
```
### Request Body

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `products` | `[product Id]` | **Required** Array of product Ids|
| `address` | `string` | **Required** |

#### My Orders (Authentication required)

```http
  GET /api/orders?page=1&limit=10
```

#### Request Query Params 
| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `page`      | `number` | **Required**. current page number  |
| `limit`      | `number` | **Required**. no of record to fetch  |

#### Get Order Details (Authentication Required)

```http
  GET /api/orders/:id
```
#### Request Params 
| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `id`      | `string` | **Required**. Id of order to Get order details  |


#### Get All Orders (Authentication required & User Must Be Admin)

```http
  GET /api/orders/all?page=1&limit=10
```

#### Request Query Params 
| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `page`      | `number` | **Required**. current page number  |
| `limit`      | `number` | **Required**. no of record to fetch  |


#### Update Order Status (Authentication required & User Should be Admin)

```http
  PUT /api/orders/:id
```
#### Request Params 
| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `id`      | `string` | **Required**. Id of product to update  |

### Request Body

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `status` | `string` | **Required** ("pending", "processing", "shipped", "delivered", "cancelled") |





