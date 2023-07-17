# DNS resolving details

## With Certificate

```mermaid
sequenceDiagram
    participant User as User
    participant DNS as DNS Resolver
    participant Route53 as Amazon Route 53
    participant CloudFront as Amazon CloudFront

    User->>DNS: Request for synth-stage.com
    DNS->>Route53: Query for synth-stage.com
    Route53-->>DNS: Alias record of CloudFront distribution domain
    DNS-->>User: Provides CloudFront distribution domain
    User->>CloudFront: Request for website
    CloudFront-->>User: Responds with website content
```

## No certificate

```mermaid
sequenceDiagram
    participant User as User
    participant DNS as DNS Resolver
    participant Route53 as Amazon Route 53
    participant CloudFront as Amazon CloudFront

    User->>DNS: Request for synth-stage.com
    DNS->>Route53: Query for synth-stage.com
    Route53-->>DNS: Alias record of CloudFront distribution domain
    DNS-->>User: Provides CloudFront distribution domain
    User->>CloudFront: Request for website
    Note over CloudFront,User: No HTTPS, communication is not secure
    CloudFront-->>User: Responds with website content
```

## Without cloudfront at all

```mermaid
sequenceDiagram
    participant User as User
    participant DNS as DNS Resolver
    participant Route53 as Amazon Route 53
    participant S3 as Amazon S3 Bucket

    User->>DNS: Request for synth-stage.com
    DNS->>Route53: Query for synth-stage.com
    Route53-->>DNS: Alias record (s3-website-us-east-1.amazonaws.com)
    DNS-->>User: Provides S3 bucket address
    User->>S3: Request for website
    Note over S3,User: No HTTPS, communication is not secure
    S3-->>User: Responds with website content
```

Secure Sockets Layer/Transport Layer Security (SSL/TLS) certificates cannot be associated with a bucket url and a custom domain. You can serve directly from the bucket over https though. You just can't add a custom domain to the bucket securely, you need to add it to cloudfront and serve the bucket over cloudfront.
