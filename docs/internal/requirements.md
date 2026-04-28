# Software Requirements Specification
**PROJECT:** Butterfly Web Application
**VERSION:** 1.0.0
**DATE:** April 2026

---

# Table of Contents

- [[#1. Introduction]]
	- [[#1.1 Purpose]]
	- [[#1.2 Scope]]
	- [[#1.3 Definitions]]
	- [[#1.4 References]]
	- [[#1.5 Overview]]
- [[#2. Overall Description]]
	- [[#2.1 Product Perspective]]
	- [[#2.2 Product Functions]]
	- [[#2.3 User Classes and Characteristics]]
	- [[#2.4 Operating Environment]]
	- [[#2.5 Constraints, Assumptions and Dependencies]]
	- [[#2.6 User Documentation]]
- [[#3. Specific Requirements]]
	- [[#3.1 External Interfaces]]
	- [[#3.2 Functionality]]
	- [[#3.3 Performance]]
	- [[#3.4 Scalability]]
	- [[#3.5 Security]]
	- [[#3.6 Availability and Reliability]]
	- [[#3.7 Usability]]
	- [[#3.8 Maintainability]]
	- [[#3.9 Observability and Monitoring]]
	- [[#3.10 Data Requirements]]
	- [[#3.11 Business Rules]]
	- [[#3.12 Regulatory]]
- [[#Appendix]]
	- [[#A.1 Data Dictionary]]

---
# 1. Introduction

## 1.1 Purpose
This document provides a detailed description of the requirements for **Butterfly**, a microblogging social media application that allows users to create accounts, publish posts, follow other users, and interact through likes, mentions and replies.

The purpose of this document is to:
- Define the functional and non-functional requirements of the system.
- Provide a reference for all developers, designers, testers, and stakeholders.
- Serve as the blueprint for system design, development, validation, and maintenance.

---
## 1.2 Scope
The system described in this document is a web-based social networking platform that enables users to publish short-form textual posts and interact with other users.

### 1.2.1 Expected Functionality
The platform shall support functions including:
- User account creation and customization.
- User authentication.
- Posting short messages, optionally with images, tags, links and mentions.
- Following users.
- Liking and replying to posts.
- Post listings.
- Searching for users and posts.

### 1.2.2 Application Contents
#### 1.2.2.1 Client Interfaces
- Web browser interface
- REST API for backend communication
  
#### 1.2.2.2 Backend Services
- User account management
- Post management
- Like management
- Follower management
- Image management
  
#### 1.2.2.3 Data Storage
- User profiles
- Posts, replies
- Likes
- Follow relationships
- User images

### 1.2.3 Out of Scope
The following features shall not be included in the current version of Butterfly.
- User notifications.
- UI language selection.
- Private messages.
- User content translation.

## 1.3 Definitions
### 1.3.1 Language Conventions

**SHALL**: Indicates a mandatory system requirement.
**SHALL NOT**: Indicates a prohibited system behavior.
**SHOULD**: Indicates a recommended requirement.
**SHOULD NOT**: Indicates discouraged behavior.
**MAY**: Indicates optional functionality.

### 1.3.2 Application Language

**Biography**: A short text that the user sets to describe themselves.
**Post**: A short user-generated message published on the platform.
**Listing**: A view displaying posts in a list.
**Follow**: A relationship where a user subscribes to another user’s posts.
**Follower**: A user that follows another user.
**Followed**: A user that is followed by another user.
**Reply**: A post that references another post.
**Like**: A user interaction indicating approval of a post.
**Unlike**: A user interaction removing approval from a post.
**Mention**: A reference to a user in a post or biography.
**Topic**: A category to which many posts refer to.
**Tag**: A reference to specific topic in posts or biographies.
**Microblogging**: A form of online publishing that allows users to post short textual updates that may include links, images, mentions and tags.
**Account**: A registered identity representing a user within the system.
**Profile**: The collection of public information associated with a user account.
**Post Listing**: A paginated collection of posts displayed in chronological order.
**Interaction**: A user action performed on another user or post, including likes, replies, and follows.
**Public Content**: Content accessible without authentication.


### 1.3.3 System Language

**Client**: A software component that interacts with backend services through APIs to present functionality to users.
**Server**: A software component that processes requests from clients and provides responses or services.
**Service**: A deployable software component responsible for a specific domain capability within the system.
**Domain**: The subject area on which an application is intended to apply.
**Projection**: A read-optimized representation of domain data derived from events.
**Event**: A message describing a state change that is published for other services to consume.
**Event Streaming Platform**: Infrastructure responsible for transporting domain events between services asynchronously.
**Message Broker**: Middleware that enables services to communicate by exchanging messages asynchronously.
**Event-driven Architecture**: An architectural style in which system components communicate primarily through events.
**Client-server Model**: An architecture where clients request services and servers provide them.
**API (Application Programming Interface)**:  Interfaces through which services communicate.
**API Gateway**: A service that acts as a single entry point for client requests and routes them to internal services.
**Public API**: An externally accessible interface exposed to clients for interacting with system functionality.
**Internal Service**: A service intended to be accessed only by other services within the system.
**Reverse Proxy**: A server that forwards client requests to backend services and returns their responses.
**Ingress Controller**: A component responsible for managing external access to services within a containerized environment.
**Container**: An executable package containing application code and its dependencies.
**Container Orchestration Platform**: Infrastructure responsible for deploying, scaling and managing containers.
**Cloud Infrastructure Provider**: A third-party platform offering computing resources such as storage, networking and servers.
**Persistent Data Layer**: Storage infrastructure responsible for long-term retention of application data.
**Relational Database**: A structured data storage system that organizes information into tables with relationships between them.
**IO**: Input and output.
**Indexing**: A technique used to improve database query performance by creating lookup structures.
**Caching**: Temporary storage of frequently accessed data to improve performance.
**DTO (Data Transfer Object)**: A structured representation of projection data optimized for client consumption.
**Schema Evolution**: The process of modifying data structures while maintaining compatibility with existing versions.
**Structured Logs**: Logs formatted in a machine-readable structure to support querying and analysis.
**Correlation Identifier**: A unique identifier attached to requests to enable tracing across services.
**Distributed Tracing**: Tracking a request as it travels across multiple services.
**Metrics**: Quantitative measurements used to monitor system behavior.
**Throughput**: The number of processed requests within a given time period.
**Latency**: The time required to process a request.
**Alert Threshold**: A predefined limit that triggers operator notification when exceeded.
**Monitoring System**: A service that collects metrics and logs to observe system health.
**Verification Token**: A credential used to confirm ownership of an email address.
**Rate Limiting**: A mechanism that restricts how frequently requests may be performed.
**Captcha**: A challenge-response mechanism used to distinguish human users from automated systems.
**CSRF (Cross-Site Request Forgery) Protection**: Mechanisms preventing unauthorized commands from being transmitted from a user’s browser.
**XSS (Cross-Site Scripting)**: A vulnerability allowing attackers to inject malicious scripts into web pages.
**UI**: User interface.
**UX**: User experience.
**Injection Attack**: A vulnerability allowing attackers to insert malicious input into a system command or query.
**MIME Type**: A standardized identifier describing the format of a file transmitted over the internet.
**Virus Scanning**: Automated inspection of uploaded files to detect malicious software.
**Load Balancing**: Distribution of incoming requests across multiple service instances.
**Horizontal Scaling**: Increasing system capacity by adding more service instances.
**Availability**: The proportion of time a system remains operational.
**Reliability**: The ability of a system to operate without failure over time.
**Eventually Consistent**: A projection that may temporarily differ from domain state but converges over time.
**Retry-safe Operation**: An operation that can be executed multiple times without unintended side effects.
**Request Identifier**: A unique identifier attached to commands to support idempotency.
**Idempotent Operation**: An operation that produces the same result when executed multiple times.
**Content Moderation**: Automated validation ensuring content complies with platform policies.
**Thumbnail**: A reduced-size representation of an image used for previews.
**Object Storage**: External storage system used to store binary files such as images.
**Object Key**: A unique identifier referencing a stored object in object storage.
**Audit Log**: A record capturing security-relevant or moderation-relevant system actions.
**Stop Words**: Common words ignored during search indexing to improve search relevance.
**Prefix Match**: A search match where the result begins with the query term.
**Suffix Match**: A search match where the result ends with the query term.
**Substring Match**: A search match where the result contains the query term anywhere within it.
**Chronological Order**: Ordering based on time of creation.
**Alphabetical Order**: Ordering based on lexicographic character sequence.
**Escaped Pattern**: A syntactic sequence intentionally marked to prevent interpretation as structured content.

---
## 1.4 References
### 1.4.1 Product Requirements Document
- [Product Requirements Document](./PRD.md)
### 1.4.2 IEEE SRS Specification
- [IEEE 830 Software Requirements Specification](https://cengproject.cankaya.edu.tr/wp-content/uploads/sites/10/2017/12/SRS-ieee-830-1998.pdf)
### 1.4.3 RFC 5322 (Email Format)
- [RFC 5322 § Addr-Spec Specification](https://datatracker.ietf.org/doc/html/rfc5322#section-3.4.1)
### 1.4.4 RFC 1738 (URL Format)
- [RFC 1738](https://datatracker.ietf.org/doc/html/rfc1738)
### 1.4.5 ISO 8601 (Date and Time Format)
- [[https://www.iso.org/iso-8601-date-and-time-format.html]]
### 1.4.6 OpenBSD (BCrypt)
- [[https://www.openbsd.org/papers/bcrypt-paper.pdf]]
### 1.4.7 WCAG 2.1 Level AA (Accessibility)
- https://www.w3.org/TR/WCAG21/
### 1.4.8 UUID (Unique ID)
- https://www.rfc-editor.org/rfc/rfc9562
### 1.4.9 OpenGraph (Sharing)
- https://ogp.me

---
## 1.5 Overview
The remainder of this document is organized as follows:
- **Section 2** describes the overall system context, product perspective, and user characteristics.
- **Section 3** defines the detailed functional and non-functional requirements of the system.

---
# 2. Overall Description

## 2.1 Product Perspective

The **Butterfly** platform is a **social media system** consisting of client applications and backend services.

The architecture shall follow a **client-server model**, where:
- Clients interact with the system through web interfaces on mobile or desktop.
- Backend services expose APIs for authentication, post management and interactions.
- A persistent data layer stores user and content information.

### 2.1.1 High-Level Architecture Components

#### 2.1.1.1 Client Layer
- Responsive web application
- Public API
#### 2.1.1.2 Application Layer
- API Gateway
- User service
- Post service
- Interaction service
- Projection service
#### 2.1.1.3 Data Layer
- User database
- Post database
- Interaction database
- Projection database
#### 2.1.1.4 External Integrations
- Email service for account verification
- Content moderation
- Image Storage
#### 2.1.1.4 Infrastructure
- Reverse proxy / ingress controller
- Distributed event streaming platform
- Container orchestration platform

### 2.1.2 Architectural Style
The system shall follow an event-driven microservice architecture.
Write operations are handled by domain services:
- User Service
- Post Service
- Interaction Service

These services publish domain events to a message broker.

Projection service maintains projections and builds DTOs. All read requests are served exclusively by this service. Write services shall not serve client read requests directly.

### 2.1.3 Messaging Infrastructure
Services shall communicate asynchronously using a distributed event streaming platform.

### 2.1.4 Service Responsibilities
#### 2.1.4.1 User Service
- Owns accounts and user images.
- Publishes user account updates.
#### 2.1.4.2 Post Service
- Owns posts and replies
- Publishes post updates.
#### 2.1.4.3 Interaction Service
- Owns likes and follows.
- Publishes like and follow updates.
#### 2.1.4.4 Projection Service
- Owns DTOs.
## 2.2 Product Functions
The system shall provide the following capabilities:
### 2.2.1 User Management
- User registration.
- User login and logout.
- Profile management.
### 2.2.2 Posting System
- Create posts.
- Delete posts.
### 2.2.3 Social Interaction
- Follow users.
- Unfollow users.
- Like posts.
- Reply to posts.
  
### 2.2.4 Listings
- Display posts from followed users.
- Display replies in post views.
  
### 2.2.5 Search
- Search users by username or display name.
- Search posts by tags.
  
### 2.2.6 Content Moderation
- Validation of images and text content according to the specified guidelines.
  
## 2.3 User Classes and Characteristics
### 2.3.1 Guest Users
Users without an account.

**Capabilities**:
- View public posts
- View user profiles
- Search public content

### 2.3.2 Registered Users Awaiting Email Verification
Users that have created an account but have not verified their email.

**Capabilities**:
- Verify email.
- Request verification mail.

### 2.3.3 Registered Users
Users with verified email.

**Capabilities**:
- Authentication.
- Create posts.
- Follow other users.
- Like and reply to posts.
- Manage profile.

### 2.3.4 Operators
Individuals that monitor and maintain the application.

**Capabilities**:
- Get notified about risky application states.

---
## 2.4 Operating Environment
The system shall operate in the following environment.
### 2.4.1 Client Platforms
- Modern web browsers (Chrome, Firefox, Safari, Edge, Opera).
- Mobile browsers.
### 2.4.2 Server Environment
- Linux-based cloud servers.
- Containerized services.
- Cloud infrastructure provider.
### 2.4.3 Database Systems
- Relational database.

---
## 2.5 Constraints, Assumptions and Dependencies
The system shall adhere to the following constraints.
- HTTPS required for all communications.
- Internal services are not accessed directly.
- Scalability requirements to support growth.
- Secure authentication and password storage.
- Content is moderated automatically.

The system shall function based on the following assumptions.
- Users have reliable internet access and email accounts.
- Email services are available for verification and notifications.
- Cloud infrastructure provides necessary scalability.

The system's functionality depends on the following.
- Image storage
- Email service
- Content moderation

---
## 2.6 User Documentation
The system shall provide:
- User help documentation.
- Account management guides.
- API documentation for developers.

---
# 3. Specific Requirements
## 3.1 External Interfaces
This section defines all interfaces between the system and external entities.
### 3.1.1 User Interfaces
This section describes the interfaces through which users interact with the system.
#### 3.1.1.1 General UI Requirements
##### NFR-EIUI-001
The system shall provide a web-based user interface accessible through modern web browsers.
##### NFR-EIUI-002
The system shall support responsive layouts for both desktop and mobile screen sizes.
##### NFR-EIUI-003
The system shall provide clear feedback for all user actions, including success and error states.
##### NFR-EIUI-004
The system shall display validation errors in a user-readable format.

#### 3.1.1.2 Authentication Interfaces
##### 3.1.1.2.1 Sign Up Interface
###### NFR-EIUA-001
The system shall provide an interface for user registration.
###### NFR-EIUA-002
The interface shall allow users to input:
   - Display name
   - Username
   - Email
   - Password
###### NFR-EIUA-003
The system shall display validation errors for invalid or missing inputs.
###### NFR-EIUA-004
Upon successful submission, the system shall display a message indicating that email verification is required.

##### 3.1.1.2.2 Sign In Interface
###### NFR-EIUA-005
The system shall provide an interface for user authentication.
###### NFR-EIUA-006
The interface shall allow users to input:
- Email
- Password
###### NFR-EIUA-007
The system shall display an error message if authentication fails.

#### 3.1.1.3 Post Interfaces
##### 3.1.1.3.1 Post Creation
###### NFR-EIUP-001
The system shall provide an interface for creating posts.
###### NFR-EIUP-002
The interface shall allow users to input post content (see [[#DDSF-010 – Post Content]]) and attach images.
###### NFR-EIUP-003
The system shall prevent submission of invalid posts as defined in the functional requirements.

##### 3.1.1.3.2 Post Listing
###### NFR-EIUP-004
The system shall display posts in a list format.
###### NFR-EIUP-005
Each post in the list shall display:
- Author information
- Content
- Creation timestamp
- Interaction counts
- Interaction actions

#### 3.1.1.4 Navigation Behavior
##### NFR-EIUN-001
The system shall allow users to access a detailed view of a post from a listing.
##### NFR-EIUN-002
The system shall allow users to access a user profile from user references.
##### NFR-EIUN-003
The system shall allow users to access a post's replies from a post preview.
##### NFR-EIUN-004
The system shall allow users to access a post listing by tag from tag references.
#### 3.1.1.5 Sharing
##### NFR-EISH-001
The system shall allow users to share specific posts, tag listings and user profiles.
##### NFR-EISH-002
The system shall ensure that public pages conform to [[#1.4.9 OpenGraph (Sharing)]] to allow display previews of content for links shared on social media.

### 3.1.2 Hardware Interfaces
This section defines interactions between the system and physical hardware.
#### NFR-EIHW-001
The system shall operate in web browsers on client devices including desktops, laptops, tablets, and smartphones.
#### NFR-EIHW-002
The system shall not require specialized hardware beyond standard IO devices (keyboard, mouse, screen and touchscreen).
#### NFR-EIHW-003
The system shall support image upload from client devices.
#### NFR-EIHW-004
The system shall access device storage only for user-initiated file selection.

### 3.1.3 Software Interfaces
This section defines interactions with external software systems and internal subsystems.
#### 3.1.3.1 API Interface
##### NFR-SWAP-001
The system shall expose a programmatic interface for client interaction.
##### NFR-SWAP-002
The interface shall return responses in JSON format.
##### NFR-SWAP-003
The system shall validate all incoming requests according to the functional requirements.

#### 3.1.3.2 Email Service
##### NFR-SWES-001
The system shall integrate with an external email service for account verification.
##### NFR-SWES-002
The system shall use email to notify users.

#### 3.1.3.3 Image Storage
##### NFR-SWIS-001
The system shall integrate with an external image storage service.
##### NFR-SWIS-002
The system shall store and retrieve user-uploaded images through this service.

### 3.1.4 Communications Interfaces
This section defines how data is transmitted between system components and external systems.
#### NFR-EICM-001
The system shall communicate over HTTPS for all external communications.
#### NFR-EICM-002
The system shall ensure all transmitted data is encrypted in transit.
#### NFR-EICM-003
The system shall support standard HTTP methods for internal communication.
#### NFR-EICM-004
The system shall upgrade public HTTP connections to HTTPS.
#### NFR-EICM-005
The system shall return appropriate status indicators for all responses.
#### NFR-EICM-006
The system shall support stateless communication between client and server.

---
## 3.2 Functionality
### 3.2.1 Account Registration
Creates an account for a new user awaiting verification.
#### FR-ACRG-001
The system shall allow the user to create an account and receive a verification mail.
#### FR-ACRG-002
The system shall require that the user is not authenticated, or send an error (see [[#DDER-002 – Message Error]]).
#### FR-ACRG-003
The system shall receive an account create request parameter that conforms to [[#DDIO-004 – Account Create Request]].
#### FR-ACRG-004
The system shall verify that the email is not already associated with an existing account.
#### FR-ACRG-005
If the email is already associated with an account, the system shall return an error (see [[#DDER-001 – Input Validation Error]]) indicating this.
#### FR-ACRG-006
The system shall verify that the username is not already associated with an existing account.
#### FR-ACRG-007
If the username is already associated with an account, the system shall return an error (see [[#DDER-001 – Input Validation Error]]) indicating this.
#### FR-ACRG-008
The system shall create a new user as specified in [[#DDDE-001 – User Account]].
#### FR-ACRG-009
The system shall start email verification as specified in [[#3.2.43 Email Verification]].
#### FR-ACRG-010
The system shall store the account indicating that the email is not verified.
#### FR-ACRG-011
The system shall send back a message (see [[#DDOO-001 – Message]]) indicating the user to check their email.

### 3.2.2 Account Email Verification
Verifies an account for a user after they interacted with verification mail.
#### FR-ACEV-001
The system shall allow a user to verify their account by responding to the verification mail sent during account creation.
#### FR-ACEV-002
The system shall require that the user is not authenticated, or send an error (see [[#DDER-002 – Message Error]]).
#### FR-ACEV-003
The system shall receive an email verification token that conforms to [[#DDSF-018 – Token]].
#### FR-ACEV-004
The system shall verify that the received email token corresponds to a stored email token.
#### FR-ACEV-005
If no stored token exists for the current token, the system shall return an error (see [[#DDER-002 – Message Error]]) indicating this.
#### FR-ACEV-006
The system shall verify that the stored token corresponds to an account with unverified email.
#### FR-ACEV-007
If no account with unverified email exists for the current token, the system shall return an error (see [[#DDER-002 – Message Error]]) indicating this.
#### FR-ACEV-008
If the current token has expired, the system shall restart verification as specified in [[#3.2.43 Email Verification]].
#### FR-ACEV-009
If the stored token has expired, the system shall delete it.
#### FR-ACEV-010
The system shall signal that the account's email has been verified.
#### FR-ACEV-011
The system shall delete the stored email verification token.

### 3.2.3 Account Verification Email Request
Request an email verification mail for an existing account with unverified email.
#### FR-AVER-001
The system shall allow a user with an unverified email to request an email verification email.
#### FR-AVER-002
The system shall require that the user is not authenticated, or send an error (see [[#DDER-002 – Message Error]]).
#### FR-AVER-003
The system shall receive an email address that conforms to [[#DDSF-008 – Email Address]].
#### FR-AVER-004
The system shall verify the email address corresponds to an account with unverified email.
#### FR-AVER-005
If no account with unverified email exists for the provided email address, the system shall return an error (see [[#DDER-002 – Message Error]]) indicating this.
#### FR-AVER-006
The system shall start email verification as specified in [[#3.2.43 Email Verification]].
#### FR-AVER-007
The system shall send back a message (see [[#DDOO-001 – Message]]) indicating the user to check their email.
### 3.2.4 Account Deletion
Deletes the account of the current user.
#### FR-ACDE-001
The system shall allow the current user to delete their account.
#### FR-ACDE-002
The system shall require that the current user is authenticated.
#### FR-ACDE-003
The system shall revoke authentication for the user.
#### FR-ACDE-004
The system shall delete all data that is account dependent from the database.
#### FR-ACDE-005
The system shall delete the account from the database.

### 3.2.5 User – Login
Authenticates the current user.
#### FR-USLI-001
The system shall allow the current user to login with email and password.
#### FR-USLI-002
The system shall receive a login request parameter that conforms to [[#DDIO-005 – Login Request]].
#### FR-USLI-003
If no account exists for the specified email, the system shall return an error (see [[#DDER-002 – Message Error]]) indicating this.
#### FR-USLI-004
If the account exists but is not validated, the system shall return an error (see [[#DDER-002 – Message Error]]) indicating this.
#### FR-USLI-005
The system shall require that the user is not authenticated, or send an error (see [[#DDER-002 – Message Error]]).
#### FR-USLI-006
If the password is invalid for the account associated with the email, the system shall return an error (see [[#DDER-002 – Message Error]]) indicating this.
#### FR-USLI-007
The system shall authenticate the current user.

### 3.2.6 User – Log Out
Revokes authentication for the current user.
#### FR-USLO-001
The system shall allow the current user to log out.
#### FR-USLO-002
The system shall require that the current user is authenticated.
#### FR-USLO-003
The system shall revoke authentication for the user.

### 3.2.7 User Profile – Get Self
Returns the user profile for the current user.
#### FR-UPGS-001
The system shall allow the current user to retrieve their profile.
#### FR-UPGS-002
The system shall require that the current user is authenticated.
#### FR-UPGS-003
The system shall return the profile (see [[#DDOO-002 – User Profile]]) of the current user.

### 3.2.8 User Profile – Get Biography
Gets a specific user's biography.
#### FR-UPGB-001
The system shall allow the current user to get another user's biography.
#### FR-UPGB-002
The system shall receive a username parameter that conforms to [[#DDSF-003 – Username]].
#### FR-UPGB-003
If no account exists for the specified username, the system shall return an error (see [[#DDER-002 – Message Error]]) indicating this.
#### FR-UPGB-004
The system shall return the specified user's biography (see [[#DDOO-006 – Biography]]).
### 3.2.9 User Profile – Set Biography
Set the biography for the current user.
#### FR-UPSB-001
The system shall allow the current user to set or change their biography.
#### FR-UPSB-002
The system shall require that the current user is authenticated.
#### FR-UPSB-003
The system shall receive a biography parameter that conforms to [[#DDSF-006 – Biography]].
#### FR-UPSB-004
The system shall parse the biography as specified in [[#3.2.32 Content Parsing]].
#### FR-UPSB-005
The system shall store or update the parsed biography separately as specified in [[#DDDE-014 – User Biography]].
#### FR-UPSB-006
The system shall update the biography of the current user.

### 3.2.10 User Profile – Set Profile Picture
Set the profile picture for the current user.
#### FR-UPSP-001
The system shall allow the current user to set or change their profile picture.
#### FR-UPSP-002
The system shall require that the current user is authenticated.
#### FR-UPSP-003
The system shall receive an image format parameter that conforms to [[#DDIO-001 – Image]].
#### FR-UPSP-004
The system shall process the image according to [[#3.2.40 Image Processing]]
#### FR-UPSP-005
The system shall set the account profile picture.

### 3.2.11 User Profile – Set Cover Picture
Set the cover picture for the current user.
#### FR-UPSC-001
The system shall allow the current user to set or update their cover picture.
#### FR-UPSC-002
The system shall require that the current user is authenticated.
#### FR-UPSC-003
The system shall receive an image format parameter that conforms to [[#DDIO-001 – Image]].
#### FR-UPSC-004
The system shall process the image according to [[#3.2.40 Image Processing]].
#### FR-UPSC-005
The system shall set the account cover picture.

### 3.2.12 User Profile – Change Username
Change the username for the current user.
#### FR-UPCU-001
The system shall allow the current user to update their username.
#### FR-UPCU-002
The system shall require that the current user is authenticated.
#### FR-UPCU-003
The system shall receive a username format parameter that conforms to [[#DDSF-003 – Username]].
#### FR-UPCU-004
If the username is already associated with an account, the system shall return an error (see [[#DDER-001 – Input Validation Error]]) indicating this.
#### FR-UPCU-005
The system shall update the account username.
### 3.2.13 User Profile – Change Display Name
Change the display name for the current user.
#### FR-UPCD-001
The system shall allow the current user to update their display name.
#### FR-UPCD-002
The system shall require that the current user is authenticated.
#### FR-UPCD-003
The system shall receive a display name format parameter that conforms to [[#DDSF-004 – Display Name]].
#### FR-UPCD-004
The system shall update the account display name.
### 3.2.14 User Profile – Get Profile
Gets a specific user's profile.
#### FR-UPGP-001
The system shall allow the current user to get another user's profile.
#### FR-UPGP-002
The system shall receive a username parameter that conforms to [[#DDSF-003 – Username]].
#### FR-UPGP-003
If no account exists for the specified username, the system shall return an error (see [[#DDER-002 – Message Error]]) indicating this.
#### FR-UPGP-004
The system shall return the specified user's profile (see [[#DDOO-002 – User Profile]]).

### 3.2.15 Post – Get
Gets a post by ID.
#### FR-POGP-001
The system shall allow the current user to get a post by ID.
#### FR-POGP-002
The system shall receive a post ID parameter that conforms to [[#DDSF-001 – Identifier]].
#### FR-POGP-003
If no post exists for the specified post ID, the system shall return an error (see [[#DDER-002 – Message Error]]) indicating this.
#### FR-POGP-004
The system shall return the specified post (see [[#DDOO-003 – Post]]).

### 3.2.16 Post – Create
Create a new post by the current user.
#### FR-POCR-001
The system shall allow the current user to create a post.
#### FR-POCR-002
The system shall require that the current user is authenticated.
#### FR-POCR-003
The system shall receive a post create request parameter that conforms to [[#DDIO-002 – Post Create Request]].
#### FR-POCR-004
The system shall parse the post content as specified in [[#3.2.32 Content Parsing]].
#### FR-POCR-005
The system shall create a new post for the current user as specified in [[#DDDE-003 – Post]].
#### FR-POCR-006
The system shall store the parsed content separately as specified in [[#DDDE-013 – Post Content]].
#### FR-POCR-007
If the request had a parent ID, the system shall mark the post as a reply as specified in [[#DDDE-011 – Post Reply]].

### 3.2.17 Post – Update
Updates a specific post.
#### FR-POUP-001
The system shall allow the current user to update their own post by ID.
#### FR-POUP-002
The system shall require that the current user is authenticated.
#### FR-POUP-003
The system shall receive a post update request parameter that conforms to [[#DDIO-003 – Post Update Request]].
#### FR-POUP-004
If the target post does not exist, the system shall return an error indicating this as specified in [[#DDER-002 – Message Error]].
#### FR-POUP-005
If the target post does not belong to the current user, the system shall return an error indicating this as specified in [[#DDER-002 – Message Error]].
#### FR-POUP-006
The system shall parse the updated post content as specified in [[#3.2.32 Content Parsing]].
#### FR-POUP-007
The system shall update the post to match the new structure specified in the post update request parameter.
#### FR-POUP-008
The system shall update the parsed content.
#### FR-POUP-009
The system shall erase all unused data (mentions, links, tags, images) after content updates.

### 3.2.18 Post – Delete
Deletes a post by the current user by ID.
#### FR-PODE-001
The system shall allow the current user to delete their own post by ID.
#### FR-PODE-002
The system shall require that the current user is authenticated.
#### FR-PODE-003
The system shall receive a post ID parameter that conforms to [[#DDSF-001 – Identifier]].
#### FR-PODE-004
If no post exists for the specified post ID, the system shall return an error (see [[#DDER-002 – Message Error]]) indicating this.
#### FR-PODE-005
If the specified post ID does not belong to the current user, the system shall return an error (see [[#DDER-002 – Message Error]]) indicating this.
#### FR-PODE-006
The system shall delete the specified post.
#### FR-PODE-007
If the post had replies, the system shall indicate that the parent is deleted as specified in [[#DDDE-011 – Post Reply]].

### 3.2.19 Post – Get All
Gets all posts by pages.
#### FR-POGA-001
The system shall allow the current user to get all posts.
#### FR-POGA-002
The system shall use pagination as specified in [[#3.2.26 Pagination]].
#### FR-POGA-003
The system shall return a page containing posts (see [[#DDOO-003 – Post]]) sorted by creation date (see [[#DDSF-015 – Time]]).

### 3.2.20 Post – Get All From Followed
Gets all posts by people that the current user follows.
#### FR-POGF-001
The system shall allow the current user to get all posts from people they follow.
#### FR-POGF-002
The system shall require that the current user is authenticated.
#### FR-POGF-003
The system shall use pagination as specified in [[#3.2.26 Pagination]].
#### FR-POGF-004
The system shall return a page containing only posts (see [[#DDOO-003 – Post]]) from users that the current user follows sorted by creation date (see [[#DDSF-015 – Time]]).

### 3.2.21 Post – Get All By User
Gets all posts by a specific user.
#### FR-POGU-001
The system shall allow the current user to get all posts by a specified user.
#### FR-POGU-002
The system shall receive a username parameter that conforms to [[#DDSF-003 – Username]].
#### FR-POGU-003
If no account exists for the specified username, the system shall return an error (see [[#DDER-002 – Message Error]]) indicating this.
#### FR-POGU-004
The system shall use pagination as specified in [[#3.2.26 Pagination]].
#### FR-POGU-005
The system shall return a page containing only posts (see [[#DDOO-003 – Post]]) authored by the target user sorted by creation date (see [[#DDSF-015 – Time]]).

### 3.2.22 Post – Get All Liked By User
Gets all posts liked by a specific user.
#### FR-POGL-001
The system shall allow the current user to get all posts liked by a specified user.
#### FR-POGL-002
The system shall receive a username parameter that conforms to [[#DDSF-003 – Username]].
#### FR-POGL-003
If no account exists for the specified username, the system shall return an error (see [[#DDER-002 – Message Error]]) indicating this.
#### FR-POGL-004
The system shall use pagination as specified in [[#3.2.26 Pagination]].
#### FR-POGL-005
The system shall return a page containing only posts (see [[#DDOO-003 – Post]]) liked by the target user sorted by creation date (see [[#DDSF-015 – Time]]).

### 3.2.23 Post – Get All Posts By Tag
Gets all posts that contain a specific tag.
#### FR-POGT-001
The system shall allow the current user to get all posts that contain a specified tag.
#### FR-POGT-002
The system shall receive a tag parameter that conforms to [[#DDSF-016 – Tag]].
#### FR-POGT-003
The system shall use pagination as specified in [[#3.2.26 Pagination]].
#### FR-POGT-004
The system shall return a page containing only posts (see [[#DDOO-003 – Post]]) that contain the target tag sorted by creation date (see [[#DDSF-015 – Time]]).

### 3.2.24 Like a Post
Creates a like by the current user for a specific post.
#### FR-LKPO-001
The system shall allow the current user to like a specific post.
#### FR-LKPO-002
The system shall require that the current user is authenticated.
#### FR-LKPO-003
The system shall receive a post ID parameter that conforms to [[#DDSF-001 – Identifier]].
#### FR-LKPO-004
If no post exists for the specified post ID, the system shall return an error (see [[#DDER-002 – Message Error]]) indicating this.
#### FR-LKPO-005
If the post specified by the post ID is already liked by the current user, the system shall return an error (see [[#DDER-002 – Message Error]]) indicating this.
#### FR-LKPO-006
The system shall create a like (see [[#DDDE-004 – Like]]) from the current user to the specified post.

### 3.2.25 Unlike a Post
Removes a like by the current user for a specific post.
#### FR-DLPO-001
The system shall allow the current user to unlike a specific post.
#### FR-DLPO-002
The system shall require that the current user is authenticated.
#### FR-DLPO-003
The system shall receive a post ID parameter that conforms to [[#DDSF-001 – Identifier]].
#### FR-DLPO-004
If no post exists for the specified post ID, the system shall return an error (see [[#DDER-002 – Message Error]]) indicating this.
#### FR-DLPO-005
If the post specified by the post ID is not liked by the current user, the system shall return an error (see [[#DDER-002 – Message Error]]) indicating this.
#### FR-DLPO-006
The system shall remove the like from the current user to the specified post.

### 3.2.26 Follow a User
Creates a follow by the current user to another user.
#### FR-FOUS-001
The system shall allow the current user to follow a specific user.
#### FR-FOUS-002
The system shall require that the current user is authenticated.
#### FR-FOUS-003
The system shall receive a username parameter that conforms to [[#DDSF-003 – Username]].
#### FR-FOUS-004
If no user exists for the specified username, the system shall return an error (see [[#DDER-002 – Message Error]]) indicating this.
#### FR-FOUS-005
If the user specified by the username is already followed by the current user, the system shall return an error (see [[#DDER-002 – Message Error]]) indicating this.
#### FR-FOUS-006
The system shall create a follow (see [[#DDDE-005 – Follow]]) from the current user to the specified user.

### 3.2.27 Unfollow a User
Removes the follow by the current user to another user.
#### FR-UFUS-001
The system shall allow the current user to unfollow a specific user.
#### FR-UFUS-002
The system shall require that the current user is authenticated.
#### FR-UFUS-003
The system shall receive a username parameter that conforms to [[#DDSF-003 – Username]].
#### FR-UFUS-004
If no user exists for the specified username, the system shall return an error (see [[#DDER-002 – Message Error]]) indicating this.
#### FR-UFUS-005
If the user specified by the username is not followed by the current user, the system shall return an error (see [[#DDER-002 – Message Error]]) indicating this.
#### FR-UFUS-006
The system shall remove the follow from the current user.
### 3.2.28 Get Followers
Gets all followers of a user by pages.
#### FR-GEFS-001
The system shall allow the current user to get all follower users.
#### FR-GEFS-002
The system shall receive a username parameter that conforms to [[#DDSF-003 – Username]].
#### FR-GEFS-003
If no account exists for the specified username, the system shall return an error (see [[#DDER-002 – Message Error]]) indicating this.
#### FR-GEFS-004
The system shall use pagination as specified in [[#3.2.26 Pagination]].
#### FR-GEFS-005
The system shall return a page containing users (see [[#DDOO-002 – User Profile]]) sorted by username (see [[#DDSF-003 – Username]]).
### 3.2.29 Get Followed
Gets all followed by a user by pages.
#### FR-GEFD-001
The system shall allow users to get all users followed by a user.
#### FR-GEFD-002
The system shall receive a username parameter that conforms to [[#DDSF-003 – Username]].
#### FR-GEFD-003
If no account exists for the specified username, the system shall return an error (see [[#DDER-002 – Message Error]]) indicating this.
#### FR-GEFD-004
The system shall use pagination as specified in [[#3.2.26 Pagination]].
#### FR-GEFD-005
The system shall return a page containing the users (see [[#DDOO-002 – User Profile]]) sorted by username (see [[#DDSF-003 – Username]]).

### 3.2.30 Search for a User
Finds all users that match a string as pages.
#### FR-SRUS-001
The system shall allow the current user to search for users.
#### FR-SRUS-002
The system shall receive a user search parameter that conforms to [[#DDSF-003 – Username]] or conforms to [[#DDSF-004 – Display Name]].
#### FR-SRUS-003
The system shall use pagination as specified in [[#3.2.26 Pagination]].
#### FR-SRUS-004
The system shall return a page containing all user profiles (see [[#DDOO-002 – User Profile]]) that match the input user search parameter by the search format specified in [[#3.2.33 Search Behavior]], sorted alphabetically.

### 3.2.31 Search for a Post by Tag
Finds all posts that match a string as pages.
#### FR-SRPO-001
The system shall allow the current user to search for posts with a specific tag.
#### FR-SRPO-002
The system shall receive a tag parameter that conforms to [[#DDSF-016 – Tag]].
#### FR-SRPO-003
The system may receive parameters that define the current page.
#### FR-SRPO-004
The system shall use pagination as specified in [[#3.2.26 Pagination]].
#### FR-SRPO-005
The system shall return a page containing all posts (see [[#DDOO-003 – Post]]) that match the input tag by the search format specified in [[#3.2.33 Search Behavior]] sorted by creation date (see [[#DDSF-015 – Time]]).

### 3.2.32 Pagination
Defines the behavior for paginated results across the system.
#### FR-PAGN-001
The system may receive pagination parameters (see [[#DDIO-007 – Page Request]]).
#### FR-PAGN-002
If pagination parameters are invalid, the system shall return an error (see [[#DDER-001 – Input Validation Error]]).
#### FR-PAGN-003
If the requested page does not exist, the system shall return an empty page.
#### FR-PAGN-004
If pagination parameters are provided, the system shall return the corresponding page.
#### FR-PAGN-005
If pagination parameters are not provided, the system shall return the first page.
#### FR-PAGN-006
The system shall limit the number of results per page to a maximum of 100 items.

### 3.2.33 Input Validation
Defines how input shall be validated for the format specified in each business function.
#### FR-IVAL-001
The system shall validate all input parameters against their defined formats.
#### FR-IVAL-002
If a required parameter is missing, the system shall return an error (see [[#DDER-001 – Input Validation Error]]).
#### FR-IVAL-003
If a parameter fails format validation, the system shall return an error (see [[#DDER-001 – Input Validation Error]]).

### 3.2.34 Confirmation Messages
Specifies how actions without return types should respond.
#### FR-CFME-001
For successful actions that do not specify a return type, the system shall return a message (see [[#DDOO-001 – Message]]) confirming the action was completed.

### 3.2.35 Real-Time Communication

#### FR-RTCM-001
The system shall establish real-time communication using WebSocket connections.
#### FR-RTCM-002
The system shall allow clients to subscribe to specific contexts (see [[#DDIO-006 – Context Change Request]]).
#### FR-RTCM-003
The system shall deliver events (see [[#DDOO-004 – Context Update]]) to clients in the order they are generated per context.
#### FR-RTCM-004
The system shall ensure at-least-once delivery of WebSocket events.
#### FR-RTCM-005
The system shall support reconnection of clients.
#### FR-RTCM-006
Upon reconnection, the system should allow clients to resynchronize their state.
#### FR-RTCM-007
The system shall terminate inactive connections after a defined timeout.
#### FR-RTCM-008
The system shall limit the rate of events per connection to prevent overload.
#### FR-RTCM-009
If a client cannot process events fast enough, the system may:
- Drop non-critical events
- Require client resynchronization
#### FR-RTCM-010
If connection fails, the system should notify the user.
### 3.2.36 Content Parsing
#### FR-COPA-001
The system shall parse all rich text fields to extract:
- Mentions
- Tags
- Links
#### FR-COPA-002
The system shall validate extracted elements according to their respective formats:
- Mentions → Username format (see [[#DDSF-003 – Username]])
- Tags → Tag format (see [[#DDSF-016 – Tag]])
- Links → URL format (see [[#DDSF-007 – URL]])
#### FR-COPA-003
The system shall store parsed elements separately from raw content:
- Mentions (see [[#DDDE-006 – Post Mention]])
- Tags (see [[#DDDE-008 – Post Tag]] and [[#DDDE-007 – Tag]])
- Links (see [[#DDDE-009 – Post Link]])
#### FR-COPA-004
The system shall render parsed elements in user interfaces as interactive components:
- Mentions → link to user profiles
- Tags → link to tag listings
- Links → clickable external references
#### FR-COPA-005
The system shall ignore malformed mention, tag, or link patterns.
#### FR-COPA-006
The system shall ignore mention, tag, or link patterns that are escaped (see [[#DDSF-017 – Escape Syntax]]).
#### FR-COPA-007
Duplicate tags within the same content shall be stored only once.

### 3.2.37 Search Behavior
#### FR-SRCH-001
The system shall perform case-insensitive matching for all search operations.
#### FR-SRCH-002
The system shall support the following matching modes:
- Prefix match
- Suffix match
- Substring match
#### FR-SRCH-003
The system shall index:
- Usernames
- Display names
- Tags
#### FR-SRCH-004
The system shall rank results by the least difference between term and results.
#### FR-SRCH-005
The system shall rank results by date when collisions occur.
#### FR-SRCH-006
The system shall ignore stop words.
#### FR-SRCH-007
The system shall ensure consistency in paginated results due to search.

### 3.2.38 Listing Behavior
#### FR-LIST-001
For post listings, the system shall return results strictly by ascending or descending  chronological order.
#### FR-LIST-002
For user listings, the system shall return results strictly by ascending or descending alphabetical order.

### 3.2.39 Content Moderation
#### FR-CMOD-001
The system shall validate that post content conforms to content moderation guidelines (see [[#3.12.1 Content Moderation Guidelines]]).
#### FR-CMOD-002
The system shall validate that image uploads conform to content moderation guidelines (see [[#3.12.1 Content Moderation Guidelines]]).
#### FR-CMOD-003
If content violates moderation guidelines (see [[#3.12.1 Content Moderation Guidelines]]), the system shall reject the request and return an error (see [[#DDER-001 – Input Validation Error]]).
#### FR-CMOD-004
The system should log all moderation actions.

### 3.2.40 Image Processing
#### FR-IMPR-001
The system shall validate all uploaded images according to [[#DDIO-001 – Image]].
#### FR-IMPR-002
The system should resize images to predefined maximum dimensions.
#### FR-IMPR-003
The system should generate thumbnails for images.
#### FR-IMPR-004
The system shall associate uploaded images with their owning user.
#### FR-IMPR-005
The system shall upload the image to the external image service (see [[#3.1.3.3 Image Storage]]).
#### FR-IMPR-006
The system shall save a record of the image according to [[#DDDE-002 – User Image]].
#### FR-IMPR-007
The system shall remove unused images when they are no longer referenced.

### 3.2.41 Rate Limiting
#### FR-RATL-001
If rate limits are exceeded, the system shall return an error (see [[#DDER-002 – Message Error]]).

### 3.2.43 Email Verification
#### FR-EMVE-001
The system shall create a verification token (see [[#DDSF-018 – Token]]).
#### FR-EMVE-002
The system shall send a link containing the verification token to the provided email account.
#### FR-EMVE-003
The system shall store the verification token as specified in [[#DDDE-015 – Email Token]].

---

## 3.3 Performance
### 3.3.1 Webpage Performance

#### NFR-WBPF-001
The system shall load the web page in less than 1.5s (p90).
#### NFR-WBPF-002
The system shall update the page in less than 500ms (p90).

### 3.3.2 Server Performance
#### NFR-SVPF-001
The system shall deliver data in less than 300ms (p90).
#### NFR-SVPF-002
The system shall utilize indexing to speed up data lookup.
#### NFR-SVPF-003
The system shall utilize a cache to improve read speed.

---
## 3.4 Scalability
### NFR-SCAL-001
The system shall be able to scale horizontally to increase system capacity.
### NFR-SCAL-002
The system shall utilize load balancing to enable horizontal scaling.

---
## 3.5 Security
### NFR-SECU-001
The system shall encrypt sensitive data at rest.
### NFR-SECU-002
The system shall authenticate all protected endpoints.
### NFR-SECU-003
The system shall prevent unauthorized access to user data.
### NFR-SECU-004
The system shall implement rate limiting per user.
### NFR-SECU-005
The system shall implement rate limiting per IP.
### NFR-SECU-006
The system shall enforce CSRF protection for all state-changing operations.
### NFR-SECU-007
The system shall sanitize all data to prevent XSS and injection.
### NFR-SECU-008
The system shall do MIME validation for all uploaded images.
### NFR-SECU-009
The system should do virus scanning on all uploaded files.
### NFR-SECU-010
The system shall only permit one user role.
### NFR-SECU-011
The system should require captcha for registration.
### NFR-SECU-012
The system shall transmit all sensitive data over HTTPS using TLS.
### NFR-SECU-013
The system shall store passwords using a secure hashing algorithm (see [[1.4.6 OpenBSD (BCrypt)]]).
### NFR-SECU-014
The system shall enforce expiration for authentication tokens.
### NFR-SECU-015
The system shall enforce expiration for email verification tokens.
### NFR-SECU-016
The system should tag repeat offenders and block their IPs and/or accounts.
### NFR-SECU-017
The system shall not log messages that contain sensitive user information.
### NFR-SECU-018
The system shall only log messages containing sensitive internal information to a protected log file.
### NFR-SECU-019
The system shall not expose internal services.

---
## 3.6 Availability and Reliability
### NFR-AVRE-001
The system shall be up 99% of the time.
### NFR-AVRE-002
The system shall implement idempotency for all retry-safe operations.
### NFR-AVRE-003
Command handlers shall support idempotency via request identifiers.
### NFR-AVRE-004
The system shall ensure that data served by the projection service is eventually consistent with domain service state.

---
## 3.7 Usability
### 3.7.1 Learnability & Intuitiveness
#### NFR-UBLI-001
The system shall have all functionality readily available.
#### NFR-UBLI-002
The system shall show tips to provide information about functionality.
#### NFR-UBLI-003
The system shall inform the user that an action is ongoing or loading.

### 3.7.2 Efficiency
#### NFR-UBEF-001
The system shall verify inputs in real time, showing errors immediately.
#### NFR-UBEF-002
The system shall not require more than 2 actions for frequent actions.
#### NFR-UBEF-003
The system shall reveal changes made in the data as soon as possible.

### 3.7.3 Error Prevention & Recovery
#### NFR-UBER-001
The system shall allow users to recover from an error in a single action.
#### NFR-UBER-002
The system shall validate input in client interfaces before executing internal business logic.

### 3.7.4 Accessibility
#### NFR-UBAC-001
The system should provide a user interface that conforms to the [[#1.4.7 WCAG 2.1 Level AA (Accessibility)]] standard.
#### NFR-UBAC-002
The system shall allow dark mode in user interfaces

### 3.7.5 User Documentation & Support
#### NFR-UBDS-001
The system shall provide documentation that users can visit to learn about application features.

---
## 3.8 Maintainability
### NFR-MAIN-001
The system shall maintain independent deployment boundaries between domain services.
### NFR-MAIN-002
The system should follow pre-defined naming and formatting conventions.
### NFR-MAIN-003
The system shall version the API.
### NFR-MAIN-004
The system should include version identifiers in domain events to support schema evolution.

---
## 3.9 Observability and Monitoring

### NFR-OBMA-001
The system shall collect structured logs for all services.
### NFR-OBMA-002
The system should include correlation identifiers in all requests to enable tracing.
### NFR-OBMA-003
The system should support distributed tracing across services.
### NFR-OBMA-004
The system should collect metrics including:
- Request latency
- Error rates
- Throughput
### NFR-OBMA-005
The system shall expose metrics for monitoring systems.
### NFR-OBMA-006
The system shall define alerting thresholds for:
- High error rates
- Increased latency
- Service downtime
### NFR-OBMA-007
The system should notify operators when alert thresholds are exceeded.
### NFR-OBMA-008
The system should retain logs and metrics for a defined period.
### NFR-OBMA-009
The system shall log messages at the following levels:
- Error: failures requiring intervention
- Warn: abnormal but recoverable
- Info: lifecycle events
- Debug/Trace: diagnostic

---
## 3.10 Data Requirements

### 3.10.1 Data Persistence
#### NFR-DRDP-001
The system shall persist all user-generated content, including posts, profiles, likes, and follow relationships.
#### NFR-DRDP-002
The system shall ensure that updates to data at similar times produce the expected result.
#### NFR-DRDP-003
The system shall not allow deleted user content to be accessible through application interfaces.
#### NFR-DRDP-004
The system shall store DTOs for optimized reads.
#### NFR-DRDP-005
The system shall derive DTOs exclusively from domain events.

### 3.10.2 Data Integrity
#### NFR-DRDI-001
The system shall enforce referential integrity between related entities.
#### NFR-DRDI-002
The system shall prevent orphaned records when dependent entities are deleted.

### 3.10.3 Data Retention
#### NFR-DRDR-001
The system shall retain user data until explicitly deleted by the user or system processes.

### 3.10.4 Data Access
### NFR-DRDA-001
The system shall restrict access to user-specific to only that user.

---
## 3.11 Business Rules

### BR-001
A user may only modify or delete content that they have created.
### BR-002
A user may not follow the same user more than once.
### BR-003
A user may not like the same post more than once.
### BR-004
A deleted post shall remain visible as “deleted” if it has replies.
### BR-005
Usernames shall be unique across the system.
### BR-006
Username updates shall not invalidate the state of the system.
### BR-007
Content that is not in accordance with the policy specified in [[#3.12.1 Content Moderation Guidelines]] shall not be allowed on the platform.

---
## 3.12 Regulatory
### 3.12.1 Content Moderation Guidelines
User images, post content and user biographies shall not contain:
- Illegal content
- Explicit sexual content
- Graphic violence
- Promotion of criminal activity
- Harassment

---
# Appendix

## A.1 Data Dictionary

### A.1.1 String Formats
#### DDSF-001 – Identifier
A unique string representing an ID for the specific domain (see [[#1.4.8 UUID (Unique ID)]]).
#### DDSF-002 – Password
A string of:
- Length between 8-16 characters
- At least one uppercase letter, number and special character.
#### DDSF-003 – Username
A string of:
- Length between 4-16 characters
- All characters are lowercase.
- Only contains letters a-z in EN-US, underscore, numbers and periods.
- Starts with a letter.
- Ends with a letter or number.
#### DDSF-004 – Display Name
A string of:
- Has length between 2-16 characters
- Only contains letters of any language, spaces, underscores, numbers or periods.
- Starts with a letter
- Ends with a letter or number
#### DDSF-006 – Biography
A string that:
- Has length between 0-128 characters
- See [[#DDSF-011 – Rich Text]]
#### DDSF-007 – URL
See [[#1.4.4 RFC 1738 (URL Format)]]
#### DDSF-008 – Email Address
See [[#1.4.3 RFC 5322 (Email Format)]]
#### DDSF-009 – Object Key
A string that references an image in storage.
#### DDSF-010 – Post Content
A string that:
- Has length between 1-256 characters
- See [[#DDSF-011 – Rich Text]]
#### DDSF-011 – Rich Text
Text that contains:
- Any characters
- Mention syntax: (see [[#DDSF-013 – Mention Syntax]])
- Tag syntax: (see [[#DDSF-012 – Tag Syntax]])
- Link syntax (see [[#DDSF-014 – Link Syntax]])
- Follows content moderation rules specified in [[#3.12.1 Content Moderation Guidelines]].
#### DDSF-012 – Tag Syntax
A string like `#<tag>` _for **tag**, see:_ [[#DDSF-016 – Tag]]
#### DDSF-013 – Mention Syntax
A string like `@<username>` _for **username**, see:_ [[#DDSF-003 – Username]]
#### DDSF-014 – Link Syntax
A string like `[[<link>]]` _for **link**, see:_ [[#DDSF-007 – URL]]
#### DDSF-015 – Time
See [[#1.4.5 ISO 8601 (Date and Time Format)]]
#### DDSF-016 – Tag
A string of:
- Length between 1-16 characters
- All characters are lowercase.
- Only contains letters a-z in EN-US, underscore and numbers.
- Starts with a letter.
- Ends with a letter or number.
#### DDSF-017 – Escape Syntax
The character `\` before link, mention or tag syntax.
#### DDSF-018 – Token
A string containing an identifier for a service.

### A.1.2 Error Models
#### DDER-001 – Input Validation Error
An object containing:
- Input name
- Error message
#### DDER-002 – Message Error
An object containing:
- Error message
#### DDER-003 – Object Field Validation Error
An object containing:
- Field name
- Error message

### A.1.3 Input Objects
#### DDIO-001 – Image
A file that:
- Is either JPEG or PNG
- MIME type is an image.
- Is at least 4B
- Is at most 16MB
- Follows content regulations specified in [[#3.12.1 Content Moderation Guidelines]].
#### DDIO-002 – Post Create Request
An object containing:
- Parent ID: id (see [[#DDSF-001 – Identifier]]) or none
- Content: string (see [[#DDSF-010 – Post Content]])
- Images: list of images (see [[#DDIO-001 – Image]]) or none
#### DDIO-003 – Post Update Request
An object containing:
- Post ID: id (see [[#DDSF-001 – Identifier]]) or none
- New Content: string (see [[#DDSF-010 – Post Content]])
- Add Images: list of images (see [[#DDIO-001 – Image]]) or none
- Remove Images: list of images (see [[#DDIO-001 – Image]]) or none
#### DDIO-004 – Account Create Request
An object containing:
- Display Name: string (see [[#DDSF-004 – Display Name]])
- Username: string (see [[#DDSF-003 – Username]])
- Email: string (see [[#DDSF-008 – Email Address]])
- Password: string (see [[#DDSF-002 – Password]])
#### DDIO-005 – Login Request
An object containing:
- Email: string (see [[#DDSF-008 – Email Address]])
- Password: string (see [[#DDSF-002 – Password]])
#### DDIO-006 – Context Change Request
An object containing:
- Type: string (see [[#DDEN-001 – Context Change Type]])
#### DDIO-007 – Page Request
An object containing:
- Page: positive integer
- Size: positive integer
- Sort: string (see [[#DDEN-006 – Sort Type]])
### A.1.4 Output Objects
#### DDOO-001 – Message
An object containing:
- Message
#### DDOO-002 – User Profile
An object containing:
- ID: string (see [[#DDSF-001 – Identifier]])
- Username: string (see [[#DDSF-003 – Username]])
- Display Name: string (see [[#DDSF-004 – Display Name]])
- Profile Picture: string (see [[#DDSF-007 – URL]]) or none
- Cover Picture: a string (see [[#DDSF-007 – URL]]) or none
- Follower Count: positive integer
- Followed By Me: boolean
- Followed Count: positive integer
- Follows Me: boolean
- Is Me: boolean
#### DDOO-003 – Post
An object containing:
- ID: string (see [[#DDSF-001 – Identifier]])
- Parent: post (see [[#DDOO-003 – Post]]) or none
- Parent Is Deleted: boolean
- Author: user profile (see [[#DDOO-002 – User Profile]])
- Content: list of content pieces (see [[#DDOO-005 – Content Piece]])
- Images: list of images (see [[#DDDE-002 – User Image]]) or none
- Reply Count: positive integer
- Like Count: positive integer
- Liked By Me: boolean
- Created: string (see [[#DDSF-015 – Time]])
#### DDOO-004 – Context Update
An object containing:
- Type: string (see [[#DDEN-003 – Context Update Type]])
- Content: post (see [[#DDOO-003 – Post]]) or user (see [[#DDOO-002 – User Profile]]) or none
#### DDOO-005 – Content Piece
An object containing
- Type: string (see [[#DDEN-005 – Content Piece Type]])
- Content: string
#### DDOO-006 – Biography
An object containing:
- Content: list of content pieces (see [[#DDOO-005 – Content Piece]])
### A.1.5 Domain Entities
#### DDDE-001 – User Account
An object containing:
- ID: user ID (see [[#DDSF-001 – Identifier]])
- Username: string (see [[#DDSF-003 – Username]])
- Email: string (see [[#DDSF-008 – Email Address]])
- Password: string (see [[#DDSF-002 – Password]])
- Display Name: string (see [[#DDSF-004 – Display Name]])
- Raw Biography: string (see [[#DDSF-006 – Biography]]) or none
- Profile Picture: image ID (see [[#DDSF-001 – Identifier]]) or none
- Cover Picture: image ID (see [[#DDSF-001 – Identifier]]) or none
- Created: string (see [[#DDSF-015 – Time]])
- VerifiedEmail: boolean
#### DDDE-002 – User Image
An object containing:
- ID: string (see [[#DDSF-001 – Identifier]])
- Owner ID: user ID (see [[#DDSF-001 – Identifier]])
- Key: string (see [[#DDSF-009 – Object Key]])
- Created: string (see [[#DDSF-015 – Time]])
#### DDDE-003 – Post
An object containing:
- ID: string (see [[#DDSF-001 – Identifier]])
- Author ID: user ID (see [[#DDSF-001 – Identifier]])
- Raw Content: string (see [[#DDSF-010 – Post Content]])
- Created: string (see [[#DDSF-015 – Time]])
#### DDDE-004 – Like
An object containing:
- Post ID: post ID (see [[#DDSF-001 – Identifier]])
- Owner ID: user ID (see [[#DDSF-001 – Identifier]])
- Created: string (see [[#DDSF-015 – Time]])
#### DDDE-005 – Follow
An object containing:
- Target ID: user ID (see [[#DDSF-001 – Identifier]])
- Owner ID: user ID (see [[#DDSF-001 – Identifier]])
- Created: string (see [[#DDSF-015 – Time]])
#### DDDE-006 – Post Mention
An object containing:
- Post ID: post ID (see [[#DDSF-001 – Identifier]])
- Mentioned User ID: user ID (see [[#DDSF-001 – Identifier]])
#### DDDE-007 – Tag
An object containing:
- ID: string (see [[#DDSF-001 – Identifier]])
- Name: string (see [[#DDSF-016 – Tag]])
#### DDDE-008 – Post Tag
An object containing:
- Post ID: string (see [[#DDSF-001 – Identifier]])
- Tag ID: string (see [[#DDSF-001 – Identifier]])
#### DDDE-009 – Post Link
An object containing:
- Post ID: string (see [[#DDSF-001 – Identifier]])
- URL: string (see [[#DDSF-007 – URL]])
#### DDDE-010 – Post Image
An object containing:
- Post ID: post ID (see [[#DDSF-001 – Identifier]])
- Image ID: image ID (see [[#DDDE-002 – User Image]])
#### DDDE-011 – Post Reply
An object containing:
- Post ID: post ID (see [[#DDSF-001 – Identifier]]) or none
- Reply ID: post ID (see [[#DDSF-001 – Identifier]])
- Parent Is Deleted: boolean
#### DDDE-012 – Content Piece
An object containing
- Type: string (see [[#DDEN-005 – Content Piece Type]])
- Text: string
#### DDDE-013 – Post Content
An object containing:
- Post ID: post ID (see [[#DDSF-001 – Identifier]]) or none
- Pieces: piece array (see [[#DDDE-012 – Content Piece]])
#### DDDE-014 – User Biography
An object containing:
- User ID: post ID (see [[#DDSF-001 – Identifier]]) or none
- Pieces: piece array (see [[#DDDE-012 – Content Piece]])
#### DDDE-015 – Email Token
An object containing:
- User ID: string (see [[#DDSF-001 – Identifier]]) or none
- Token: string (see [[#DDSF-018 – Token]])
- Created: string (see [[#DDSF-015 – Time]])

### A.1.6 Enumerations
#### DDEN-001 – Context Change Type
A string that is one of:
- `listing:<type>`  _for **type**, see:_ [[#DDEN-002 – Listing Type]]
- `profile:<user ID>` _for **user ID**, see:_ [[#DDSF-001 – Identifier]]
- `post:<post ID>` _for **post ID**, see:_ [[#DDSF-001 – Identifier]]
#### DDEN-002 – Listing Type
A string that is one of:
- `all`
- `user:<user ID>` _for **user ID**, see:_ [[#DDSF-001 – Identifier]]
- `likes:<user ID>` _for **user ID**, see:_ [[#DDSF-001 – Identifier]]
- `tag:<tag>`  _for **tag**, see:_ [[#DDSF-016 – Tag]]
#### DDEN-003 – Context Update Type
A string that is one of:
- `profile:<user ID>` _for **user ID**, see:_ [[#DDSF-001 – Identifier]]
- `post:<action>:<user ID>` _for **post ID**, see:_ [[#DDSF-001 – Identifier]]
#### DDEN-004 – Post Action Type
A string that is one of:
- `create`
- `delete`
- `update`
#### DDEN-005 – Content Piece Type
A string that is one of:
- `text`
- `mention`
- `link`
- `tag`
#### DDEN-006 – Sort Type
A string that is one of:
- `asc`
- `desc`
