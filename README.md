### Stage 1:
My solution includes using kubernetes as a base, or more specfically a deployment which mounts configmaps as volumes on an nginx base image.
I use a configmap with nginx configuration as a pseudo "service" for services 'a' and 'b'.
I load the main config and prod/dev configs separately and concatenate their contents using nginx's SSI (Server Side Includes).

Attached is the yaml file including all components of the deployment I managed to create.

### Stage 2:
1. Write/describe a process for rolling an update of a new app version, and deploying it to dev and then to prod

0. Dev pushes local commits to remote
1. Dev initiates Pull Request (after code review) into dev branch
2. An automatic build starts in order to ensure that the code compiles on a well-defined env
	2.1. Build process (a job made of multiple tasks) is run via an agent running on a slave machine by the build-managing server (ADO/Jenkins...)
	2.2 The tasks such a job might include are first a clone of the code (or just a delta update of the local repository on the build server) then multiple dependency-resolving steps, compilation, unit tests, static code analysis (not necessarily in that order), and finally a deployment of the resulting artifact to artifact storage (azure artifacts/artifactory/nexus)
3. If the build succeeds, the code is successfully pushed into dev
4. Team Leader/Project Manager can then decide to push the code to master - which I will treat as the only CD branch in this example - and initiate a CD process automatically or manually.
5. The new artifact will be pulled into several environments, in specific order, to make it go through a QA process before full release into production.
	5.1. This process usually includes 3 environments:
		1. Dev
		2. Test
		3. Prod
	5.2 These environments are comprised of one or more machines running agents that register them as part of one of the 3 mentioned environments
6. Gates for approval of each stage can be set, either by automated processes, or manual approval by key personnel.






2. Write/describe a process for deployment of a configuration update (one of the values in the config file), which should trigger a restart of the app and result an update of the service response

1. Run the command
kubectl apply -f https://raw.githubusercontent.com/stakater/Reloader/master/deployments/kubernetes/reloader.yaml
2. Add configmap.reloader.stakater.com/reload: "name-of-configmap" to your deployment's annotations

3. Edit and save the configmap
