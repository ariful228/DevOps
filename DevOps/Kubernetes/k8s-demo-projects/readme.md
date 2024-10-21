
# Kubernetes Workflow Diagram

## 1. ConfigMap: `mongo-config`
- **Data**: 
  - `mongo-url`: `mongodb://mongo-service:27017`
- **Usage**: Provides MongoDB connection URL to `webapp-deployment`.

---

## 2. Secret: `mongo-secret`
- **Data**: 
  - `mongo-user`: `admin`
  - `mongo-password`: `password`
- **Usage**: Supplies sensitive information to both `mongo-deployment` and `webapp-deployment`.

---

## 3. Deployment: `mongo-deployment`
- **Replicas**: `1`
- **Container**: `mongodb`
  - **Image**: `mongo:5.0`
  - **Ports**: `27017`
  - **Environment Variables**:
    - `MONGO_INITDB_ROOT_USERNAME` → `mongo-secret/mongo-user`
    - `MONGO_INITDB_ROOT_PASSWORD` → `mongo-secret/mongo-password`
- **Service**: Exposed via `mongo-service`.

---

## 4. Service: `mongo-service`
- **Type**: `ClusterIP`
- **Selector**: `app: mongo`
- **Ports**:
  - **Port**: `27017`
  - **Target Port**: `27017`
- **Function**: Routes traffic to `mongo-deployment`.

---

## 5. Deployment: `webapp-deployment`
- **Replicas**: `1`
- **Container**: `webapp`
  - **Image**: `nanajanashia/k8s-demo-app:v1.0`
  - **Ports**: `3000`
  - **Environment Variables**:
    - `USER_NAME` → `mongo-secret/mongo-user`
    - `USER_PASSWORD` → `mongo-secret/mongo-password`
    - `DB_URL` → `mongo-config/mongo-url`
- **Service**: Exposed via `webapp-service`.

---

## 6. Service: `webapp-service`
- **Type**: `NodePort`
- **Selector**: `app: webapp`
- **Ports**:
  - **Port**: `3000`
  - **Target Port**: `3000`
  - **NodePort**: `30100`
- **Function**: Exposes the web application to external clients.

---

# Point-to-Point Connections

- **ConfigMap `mongo-config`** 
  - → **Environment Variable in `webapp-deployment`**: Provides MongoDB URL.

- **Secret `mongo-secret`** 
  - → **Environment Variables in `mongo-deployment`**: Supplies MongoDB username and password.
  
- **Secret `mongo-secret`** 
  - → **Environment Variables in `webapp-deployment`**: Supplies MongoDB username and password for the web application.

- **Deployment `mongo-deployment`** 
  - → **Service `mongo-service`**: Exposes MongoDB to other services within the cluster.

- **Deployment `webapp-deployment`** 
  - → **Service `webapp-service`**: Exposes the web application to external access.

- **Service `webapp-service`** 
  - → **External Clients**: Allows external clients to access the web application via the assigned NodePort.
