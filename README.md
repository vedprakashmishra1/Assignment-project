# Advanced Blog Service with AI Integration

A Spring Boot-based blog management system with AI-powered text summarization, Redis caching, and AWS deployment capabilities.

## Features

- RESTful APIs for blog management (CRUD operations)
- AI-powered text summarization using OpenAI GPT-3.5
- Redis caching for improved performance
- PostgreSQL database for data persistence
- JWT-based authentication (ready to implement)
- AWS S3 integration for image storage
- Docker containerization
- Pagination support

## Prerequisites

- Java 17
- Maven
- PostgreSQL
- Redis
- Docker (for containerization)
- AWS Account (for deployment)
- OpenAI API Key

## Setup Instructions

1. **Clone the repository**
```bash
git clone <repository-url>
cd blog-service
```

2. **Configure application.yml**
Update `src/main/resources/application.yml` with your credentials:
```yaml
spring:
  datasource:
    url: jdbc:postgresql://localhost:5432/blogdb
    username: your-username
    password: your-password

openai:
  api-key: your-openai-api-key

aws:
  access-key: your-aws-access-key
  secret-key: your-aws-secret-key
  s3:
    bucket: your-bucket-name
    region: your-region
```

3. **Build the application**
```bash
mvn clean package
```

4. **Run locally**
```bash
java -jar target/blog-service-0.0.1-SNAPSHOT.jar
```

## API Endpoints

### Blog Management

#### Create Blog
```http
POST /api/blogs
Content-Type: application/json

{
  "title": "Blog Title",
  "content": "Blog Content",
  "author": "Author Name",
  "imageUrl": "optional-image-url"
}
```

#### Get Blog by ID
```http
GET /api/blogs/{id}
```

#### Get All Blogs (Paginated)
```http
GET /api/blogs?page=0&size=10
```

#### Update Blog
```http
PUT /api/blogs/{id}
Content-Type: application/json

{
  "title": "Updated Title",
  "content": "Updated Content",
  "author": "Author Name",
  "imageUrl": "optional-image-url"
}
```

#### Delete Blog
```http
DELETE /api/blogs/{id}
```

## Docker Deployment

1. **Build Docker image**
```bash
docker build -t blog-service .
```

2. **Run Docker container**
```bash
docker run -p 8080:8080 blog-service
```

## AWS Deployment

1. **Configure AWS CLI with your credentials**

2. **Create ECR repository**
```bash
aws ecr create-repository --repository-name blog-service
```

3. **Push Docker image to ECR**
```bash
aws ecr get-login-password --region your-region | docker login --username AWS --password-stdin your-account-id.dkr.ecr.your-region.amazonaws.com
docker tag blog-service:latest your-account-id.dkr.ecr.your-region.amazonaws.com/blog-service:latest
docker push your-account-id.dkr.ecr.your-region.amazonaws.com/blog-service:latest
```

4. **Deploy to ECS or EC2**
- Follow AWS documentation for deploying containers to ECS or EC2

## Architecture

The application follows a layered architecture:
- Controller Layer: Handles HTTP requests
- Service Layer: Contains business logic
- Repository Layer: Manages data persistence
- Model Layer: Defines data entities
- DTO Layer: Manages data transfer objects

Key components:
- Spring Boot 3.2.3
- Spring Data JPA
- Spring Security
- Redis Caching
- OpenAI Integration
- AWS SDK
- PostgreSQL

## Performance Optimization

- Redis caching for frequently accessed blogs
- Pagination for large datasets
- AI-powered text summarization
- Efficient database indexing

## Security

- JWT-based authentication (ready to implement)
- Input validation
- Secure password handling
- HTTPS support

## Future Enhancements

1. Implement JWT authentication
2. Add user management
3. Implement comment system
4. Add blog categories and tags
5. Implement full-text search
6. Add image compression
7. Implement rate limiting
8. Add metrics and monitoring
