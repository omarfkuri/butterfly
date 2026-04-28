# Tasks

- [ ] **1. Setup**
	- [ ] Git
		- [x] Gitignore
		- [x] Readme
		- [x] GitHub
	- [ ] Contracts
		- [ ] Domain
			- [ ] User
			- [ ] Post
			- [ ] Interaction
		- [ ] Internal
			- [ ] REST
				- [ ] User
				- [ ] Post
				- [ ] Interaction
			- [ ] Events
				- [ ] User
				- [ ] Post
				- [ ] Interaction
		- [ ] Public
			- [ ] REST
			- [ ] Events

- [ ] **2. Basic infrastructure**
	- [ ] Docker Compose file
	- [ ] Develop script

	- [ ] NGINX
		- [ ] Container
			- [ ] Dockerfile
			- [ ] Docker Compose entry
		- [ ] Config
			- [ ] Frontend
			- [ ] API

	- [ ] Kafka
		- [ ] Container
			- [ ] Dockerfile
			- [ ] Docker Compose entry

- [ ] **3. Services Implementation**
	- [ ] Content parsing library
		- [ ] Spring project creation
		- [ ] Library implementation

	- [ ] User database
		- [ ] Container
			- [ ] Dockerfile
			- [ ] Docker Compose entry

	- [ ] User contract library
		- [ ] Spring project creation
		- [ ] Library implementation

	- [ ] User service
		- [ ] Spring project creation
		- [ ] Container
			- [ ] Dockerfile
			- [ ] Docker Compose entry
		- [ ] Database config
		- [ ] Application config
			- [ ] Database config
			- [ ] Kafka config
		- [ ] Service implementation
			- [ ] User entity and repository
			- [ ] Service
				- [ ] GMail integration
				- [ ] User creation and deletion
				- [ ] User profile editing
				- [ ] User query (for auth)
				- [ ] Password validation

	- [ ] Post database
		- [ ] Container
			- [ ] Dockerfile
			- [ ] Docker Compose entry

	- [ ] Post contract library
		- [ ] Spring project creation
		- [ ] Library implementation

	- [ ] Post service
		- [ ] Spring project creation
		- [ ] Container
			- [ ] Dockerfile
			- [ ] Docker Compose entry
		- [ ] Database config
		- [ ] Application config
			- [ ] Database config
			- [ ] Kafka config
		- [ ] Service implementation
			- [ ] User entity and repository
			- [ ] Service
				- [ ] GC Storage integration
				- [ ] Post creation, update and deletion
				- [ ] Image handling

	- [ ] Interaction database
		- [ ] Container
			- [ ] Dockerfile
			- [ ] Docker Compose entry

	- [ ] Interaction contract library
		- [ ] Spring project creation
		- [ ] Library implementation

	- [ ] Interaction service
		- [ ] Spring project creation
		- [ ] Container
			- [ ] Dockerfile
			- [ ] Docker Compose entry
		- [ ] Database config
		- [ ] Application config
			- [ ] Database config
			- [ ] Kafka config
		- [ ] Service implementation
			- [ ] User entity and repository
			- [ ] Service
				- [ ] Like creation and deletion
				- [ ] Follow creation and deletion

	- [ ] Redis
		- [ ] Container
			- [ ] Dockerfile
			- [ ] Docker Compose entry

	- [ ] API Gateway setup
		- [ ] Spring project creation
		- [ ] Container
			- [ ] Dockerfile
			- [ ] Docker Compose entry
		- [ ] Application config
			- [ ] User Service path
				- [ ] Path
				- [ ] Rate limiting
			- [ ] Post Service path
				- [ ] Path
				- [ ] Rate limiting
			- [ ] Interaction Service
				- [ ] Path
				- [ ] Rate limiting
		- [ ] Authentication config

	- [ ] Projection database
		- [ ] Container
			- [ ] Dockerfile
			- [ ] Docker Compose entry

	- [ ] Projection service
		- [ ] Spring project creation
		- [ ] Container
			- [ ] Dockerfile
			- [ ] Docker Compose entry
		- [ ] Database config
		- [ ] Application config
			- [ ] Database config
		- [ ] Service implementation
			- [ ] User event listener
			- [ ] User read controller
			- [ ] Post event listener
			- [ ] Post read controller
			- [ ] Interaction event listener
			- [ ] Interaction read controller
			- [ ] Real time event transmission

	- [ ] Contract tests
		- [ ] User
		- [ ] Post
		- [ ] Interaction

	- [ ] Integration tests
		- [ ] User
		- [ ] Post
		- [ ] Interaction

	- [ ] Service performance tests
			      
- [ ] **4. Frontend Implementation**
	- [ ] SvelteKit setup
	- [ ] Container
		- [ ] Dockerfile
		- [ ] Docker Compose entry
	- [ ] Contract types
	- [ ] Utilities
		- [ ] Fetching
		- [ ] Real time engine
		- [ ] Parsed content
	- [ ] Styles
	- [ ] Components
	- [ ] Pages
	- [ ] End to end tests
	      
- [ ] **5. Local Deployment**  
	- [ ] Local Kubernetes setup (Kind)
		- [ ] Install Kind
		- [ ] Cluster creation script
		- [ ] kubectl configuration

	- [ ] Local image workflow
		- [ ] Build Docker images
		- [ ] Load images into Kind cluster

	- [ ] Kubernetes manifests (dev validation)
		- [ ] Deployments
		- [ ] Services
		- [ ] ConfigMaps
		- [ ] Secrets

	- [ ] Ingress (NGINX)
		- [ ] Install ingress controller
		- [ ] Local routing
			- [ ] Frontend
			- [ ] API Gateway

	- [ ] Minimal system validation
		- [ ] API Gateway
		- [ ] One service (User)
		- [ ] End-to-end request flow

	- [ ] Debugging workflow
		- [ ] kubectl logs
		- [ ] Port-forwarding
		- [ ] Pod inspection


- [ ] **6. Observability and monitoring**
	- [ ] OpenTelemetry setup
		- [ ] Add OpenTelemetry dependencies to all services
		- [ ] Configure trace exporters
		- [ ] Instrument:
			- [ ] API Gateway
			- [ ] User Service
			- [ ] Post Service
			- [ ] Interaction Service
			- [ ] Projection Service

	- [ ] Logging
		- [ ] Loki container
			- [ ] Docker Compose entry
		- [ ] Configure log collection
			- [ ] Service logs (stdout)
			- [ ] NGINX logs
		- [ ] Log format standardization (JSON)

	- [ ] Metrics
		- [ ] Prometheus container
			- [ ] Docker Compose entry
		- [ ] Configure scrape targets
			- [ ] API Gateway
			- [ ] All services
			- [ ] Kafka
			- [ ] Redis
		- [ ] Expose metrics endpoints in services

	- [ ] Tracing
		- [ ] Tempo container
			- [ ] Docker Compose entry
		- [ ] Connect OpenTelemetry to Tempo

	- [ ] Visualization
		- [ ] Grafana container
			- [ ] Docker Compose entry
		- [ ] Configure data sources
			- [ ] Prometheus
			- [ ] Loki
			- [ ] Tempo
		- [ ] Dashboards
			- [ ] API Gateway metrics
			- [ ] Service metrics
			- [ ] Kafka metrics
			- [ ] System health overview

	- [ ] Long-term metrics
		- [ ] Mimir container
			- [ ] Docker Compose entry
		- [ ] Connect Prometheus remote write

	- [ ] Alerts
		- [ ] Define alert rules
			- [ ] High latency
			- [ ] High error rate
			- [ ] Service down
			- [ ] Kafka lag
		- [ ] Configure Alertmanager

- [ ] **7. Production Deployment
	- [ ] Google Cloud setup
		- [ ] Create project
		- [ ] Enable APIs
			- [ ] Kubernetes Engine
			- [ ] Artifact Registry
			- [ ] Cloud DNS
			- [ ] Cloud Storage
		- [ ] Configure IAM roles
		- [ ] Create service accounts

	- [ ] Container registry (Artifact Registry)
		- [ ] Create repository
		- [ ] Authenticate CI/CD
		- [ ] Push service images

	- [ ] Kubernetes cluster (GKE)
		- [ ] Create GKE Autopilot cluster
		- [ ] Configure kubectl access
		- [ ] Namespace strategy

	- [ ] Kubernetes manifests structure
		- [ ] Base
			- [ ] Deployments
			- [ ] Services
			- [ ] ConfigMaps
			- [ ] Secrets
		- [ ] Production overlays
			- [ ] Resource limits
			- [ ] Scaling configs
			- [ ] External endpoints

	- [ ] Infrastructure deployment
		- [ ] Kafka (cluster or managed alternative)
		- [ ] Redis
		- [ ] Databases (StatefulSets or managed SQL)
		- [ ] Observability stack

	- [ ] Application deployment
		- [ ] User Service
		- [ ] Post Service
		- [ ] Interaction Service
		- [ ] Projection Service
		- [ ] API Gateway
		- [ ] Frontend

	- [ ] Networking and exposure
		- [ ] Static external IP
		- [ ] Ingress controller (NGINX)
		- [ ] Routing rules
			- [ ] Frontend
			- [ ] API Gateway

	- [ ] DNS configuration
		- [ ] Register domain (external registrar)
		- [ ] Configure Cloud DNS zone
		- [ ] Create A record → static IP

	- [ ] TLS / HTTPS
		- [ ] TLS certificates (managed or cert-manager)
		- [ ] Attach certificates to ingress

	- [ ] External services (GC integrations)
		- [ ] Cloud Storage buckets
			- [ ] Image storage
			- [ ] Permissions (service account access)
		- [ ] Gmail API / SMTP setup
		- [ ] Configure service credentials in Kubernetes secrets

	- [ ] Configuration management
		- [ ] Environment variables
		- [ ] Secrets (DB credentials, JWT keys, API keys)

	- [ ] CI/CD (GitHub Actions)
		- [ ] Build pipeline
			- [ ] Build Docker images
			- [ ] Run tests
		- [ ] Deploy pipeline
			- [ ] Push images to Artifact Registry
			- [ ] Apply Kubernetes manifests

	- [ ] Health checks
		- [ ] Liveness probes
		- [ ] Readiness probes

	- [ ] Scaling
		- [ ] Horizontal Pod Autoscaler (HPA)
		- [ ] Resource requests and limits

	- [ ] Rollouts
		- [ ] Rolling updates
		- [ ] Rollback strategy

	- [ ] Backups and recovery
		- [ ] Database backups
		- [ ] Restore procedure