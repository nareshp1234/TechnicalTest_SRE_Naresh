# Commands

## Dockerfile and Docker-compose code
Working Directory : Tui_App\tuiapp
Docker-compose up

## Prometheus 
http://127.0.0.1:9090/targets

## Building Image
docker build -t tuiapp_web .

## Django Application url's :
http://127.0.0.1:8000/polls/
http://127.0.0.1:8000/admin/

Added livelinees probe in djago deployment 
Commented Liveliness probe as healthcheck is not added

## since i am using local docker image instead of repository i have used this tag.
imagepullpolicy never 

## Kubernetes code
Working Directory : Tui_App\tuiapp\deploy\kubernetes
Kubernetes files

## Steps for running kubernetes files(on minikube I have tested)
eval $(minikube docker-env)

Apply Manifests
$ kubectl apply -f postgres/
$ kubectl apply -f django/

# Show service in browser
$ minikube service django-service  # Wait if not ready




## Theoritical Part 
What deployment steps would you have in a future CI/CD pipeline? A pseudo code is
appreciated.

After creating above steps 
connecting CI tool to kubernetes cluster(for ex : jenkins)
sudo cp ~/.kube/config ~jenkins/.kube/
sudo chown -R jenkins: ~jenkins/.kube/

Create credential for dockerhub or private registry , github.

	Create jenkinsfile/Pipeline steps as below
	checkout code
	Build docker image
	Test docker image
	Push the docker image to ACR/registry
	Deploy the application using kubernetes manifest files.


Describe how you would run your application on production in a cloud environment.
	create highly available cluster with 3 master nodes in availability zones and worked nodes
	Deploy cluster on private subnets
	Worker nodes using autoscalling groups
	create EFS for storing persistent data
	using resource limits for usage of resources on each node.
	use network loadbalancer + Application loadbalancer for incomming request from users.
	behind application loadbalance have ingress+ ingress controller routing request to the cluster which will be secure with single point of entry within cluster.
	Have etcd in 3 availability zones(for high availability)
	Postgress DB can be deployed as master + worker nodes where master is used for read+ writes
	and worker DB nodes are used only as replication of master to serve request.
	monitoring cluster by running prometheus/any other tool as deamon set.
	Storing credentials in azure key vault/AWS secret manager.



• Bonus: How would you deploy and run your application across multiple regions?

