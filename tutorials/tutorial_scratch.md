---

copyright:
  years: 2016, 2019
lastupdated: "2019-09-09"

keywords: scratch, developer tools, custom app, app tutorial, basic starter kit, language, backend, mobile

subcollection: creating-apps

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}
{:note: .note}

# Creating a custom app from a basic starter kit
{: #tutorial-scratch}

You can create a custom application by using a basic starter kit and selecting the app type (mobile or backend), language, and framework. adding services, and selecting your deployment target. 
{: shortdesc}

The basic starter kit is a versatile tool that you can use to create custom apps that you define by language, app type, framework, and services. Then, you set up continuous delivery and select the deployment target of your choice.

## Before you begin
{: #prereqs-scratch}

* Install the [{{site.data.keyword.dev_cli_long}}](/docs/cli?topic=cloud-cli-getting-started), which include Docker. 
* Create a Docker account, run the Docker app, and sign in. Docker must be running for the build commands to work.
* If you plan to deploy your app to {{site.data.keyword.cfee_full}}, you must [prepare your {{site.data.keyword.cloud_notm}} account](/docs/cloud-foundry?topic=cloud-foundry-permissions).

## Creating your app
{: #create-scratch}

1. From your [{{site.data.keyword.cloud_notm}} dashboard ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}), click **Create an app** in the Apps tile.

  You can also create a custom app from the [Starter Kits ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/developer/appservice/starter-kits) page in the {{site.data.keyword.dev_console}}.
  {: tip}

2. On the App details page, enter a name for your app. For this tutorial, type `CustomApp`.
3. You can optionally provide tags to classify your app. For more information, see [Working with tags](/docs/resources?topic=resources-tag).
4. Select the **Create a new app** tile.
5. Select an app type of **Backend**.
  If you select **Mobile** as the app type, see [Creating a custom mobile app](docs/apps/tutorials?topic=creating-apps-tutorial-mobile#create-mobile-basic) for instructions.
  {: tip}
6. Select the language and framework that you want to use for your app. Some starter kits might be available in only one language.
7. Click **Create**.

Great start! You just created an app!

## Adding services (optional)
{: #resources-scratch}

You can add services that enhance your app with the cognitive power of Watson, add mobile services, or security services.

If you want to create a new service instance or connect any existing services to your app, complete these steps:

1. On the App details page, click **Create service** or **Connect existing services**, depending on whether you already have services that you want to connect to this app.
2. Select the kind of service you want, and follow the prompts to either add an existing service to your app or create a service instance. For example, select **Data** > **Next** > **Cloudant** > **Next**.
3. Select your pricing plan. You can use the free option for this tutorial.
4. Click **Create**.

After you add all the services that you want, the services are displayed in the App details page.

## Building and running the app locally
{: #build-run-scratch}

You can view your app code by clicking **Download code** on the App details page of your app. Your code is downloaded as a `.zip` file that contains the complete app code structure. You can extract the file and run the code locally by using the {{site.data.keyword.dev_cli_notm}}, or add it to your code management repository.

The app code includes a `README.md` file that contains technical details about the app. Check the `README.md` file to find out whether you need to take more actions to get your app up and running.
{: tip}

If you want to build the app locally for testing before you deploy it to the cloud, complete these steps:

1. On the **App details** page, click **Download code** to work with your code locally.
2. Import the app to your integrated development environment.
3. Modify the code.
4. Set up [Git authentication](/docs/services/ContinuousDelivery?topic=ContinuousDelivery-git_working#git_authentication) by adding a personal access token.
5. Log in to the {{site.data.keyword.cloud_notm}} command-line interface (CLI). If your organization uses federated logins, use the `-sso` option; for example:

  ```bash
  ibmcloud login -sso
  ```
  {: pre}

6. Run the following command to set your org and space targets.

  ```bash
  ibmcloud target --cf
  ```
  {: pre}

7. Run the following command to retrieve the credentials.

  ```bash
  ibmcloud dev get-credentials
  ```
  {: pre}

8. Make sure that Docker is running, and run the following command to build your app in a local development container from the directory.

  ```bash
  ibmcloud dev build
  ```
  {: pre}

9. Run the following command to run your app in a local development container.

  ```bash
  ibmcloud dev run
  ```
  {: pre}

10. Go to `http://localhost:3000` in your browser. Your port number might be different depending on your chosen runtime.

## Deploying your app
{: #deploy-scratch}

When you select a deployment target, a DevOps toolchain is automatically created for your app. The toolchain includes a Delivery Pipeline that indicates your app’s deployment status. The new app that is generated is pushed to a GitLab repo that is part of the toolchain.

Enabling a DevOps toolchain creates a team-based development environment for your app. When you create a toolchain, the app service creates a Git repository, where you can view source code, clone your app, and create and manage issues. You also have access to a dedicated GitLab environment and a continuous delivery pipeline. They're customized to the deployment target that you select.

All toolchains that are created from an {{site.data.keyword.cloud_notm}} Developer dashboard are configured for automatic deployment.
{: note}

To select your deployment target and configure continuous delivery, complete these steps:

1. On the App details page, click **Configure continuous delivery**.
2. Select a deployment target. Set up your deployment target according to the instructions for the target that you select:
  * **Deploy to [IBM Kubernetes Service](/docs/containers?topic=containers-app)**. This option creates a cluster of hosts, called worker nodes, to deploy and manage highly available app containers. You can create a cluster or deploy to an existing cluster.
  * **Deploy to Cloud Foundry**. This option deploys your cloud-native app without you needing to manage the underlying infrastructure. If your account has access to {{site.data.keyword.cfee_full_notm}}, you can select a deployer type of either **[Public Cloud](/docs/cloud-foundry-public?topic=cloud-foundry-public-deployingapps)** or **[Enterprise Environment](/docs/cloud-foundry?topic=cloud-foundry-deploy_apps)**, which you can use to create and manage isolated environments for hosting Cloud Foundry apps exclusively for your enterprise.
  * **Deploy to a [Virtual Server](/docs/vsi?topic=virtual-servers-deploying-to-a-virtual-server)**. This option provisions a virtual server instance, loads an image that includes your app, creates a DevOps toolchain, and initiates the first deployment cycle for you.

After you select and configure the deployment target, the App details page indicates that continuous delivery is configured. You can view the repo that contains the generated code for your app by clicking **View repo**.

To deploy your app with the command line, use `ibmcloud dev deploy`. For more information, see [Creating and deploying apps by using the CLI](/docs/apps?topic=creating-apps-create-deploy-app-cli).

For more information about deploying your app, see [Deploying apps](/docs/apps?topic=creating-apps-deploying-apps).

## Verifying that your app is running
{: #verify-scratch}

After your app is built and deployed, you can view the app's URL to make sure that it's running.

### Apps that are deployed to a Kubernetes cluster
{: #view-kube-app-scratch}

For apps that are deployed to a Kubernetes cluster, you can view the app's URL in either the Delivery Pipeline or the command line.

1. On the App details page, click **View toolchain**.
1. From your DevOps toolchain, click **Delivery Pipeline**, and then select **Deploy Stage**.
2. Click **View logs and history**.
3. In the log file, find the app's URL:

    At the end of the log file, search for the word `urls` or `view`. For example, you might see a line in the log file that's similar to `urls: my-app-devhost.mybluemix.net` or `View the application health at: http://<ipaddress>:<port>/health`.

4. Go to the URL in your browser. If the app is running, a message that includes `Congratulations` or `{"status":"UP"}` is displayed.

If you are using the command line, run the [`ibmcloud dev view`](/docs/cli/idt?topic=cloud-cli-idt-cli#view) command to view the URL of your app. Then, go to the URL in your browser.

### Viewing your app's Kubernetes cluster
{: #view-kube-cluster-scratch}

If you want to view the cluster where your app is deployed, click **View Kubernetes cluster** on the App details page.

### Apps that are deployed to Cloud Foundry
{: #view-cf-app-scratch}

For apps that are deployed to Cloud Foundry, you can view the app's URL from the App details page by clicking **Visit App URL**. If the app is running, a message that includes `Congratulations` is displayed.

If you are using the command line, run the [`ibmcloud dev view`](/docs/cli/idt?topic=cloud-cli-idt-cli#view) command to view the URL of your app. Then, go to the URL in your browser.
