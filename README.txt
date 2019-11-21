- This is the repository for DevOps Interview Questions. Each branch is tied to a specific scenario.
- The goal of this is to see how many branches a potential candidate can fix and deploy.
- In order to complete some of the scenarios in this Interview Hub, you'll need to download and install the Ant Migration Tool.
- Prior to installing Ant, you need to setup a demo Salesforce Developer environment.
	- https://developer.salesforce.com/signup

How to install and set up Ant:

1. Download the Ant Migration Tool from: https://developer.salesforce.com/docs/atlas.en-us.daas.meta/daas/forcemigrationtool_install.htm
2. Navigate to where your downloads are stored, and navigate to salesforce_ant_VERSION/sample
3. Copy and paste the following to the bottom of build.xml:

	<target name="build_DemoOrg">
		<sf:deploy username="${sf.usernameDemoOrg}"
			password="${sf.passwordDemoOrg}" 
			serverurl="${sf.serverUrlDemoOrg}"
			deployroot="${sf.deployRoot_DemoOrg}"
			testLevel="NoTestRun" />
	</target>

	<target name="retrieve_DemoOrg">
		<sf:retrieve username="${sf.usernameDemoOrg}" 
			password="${sf.passwordDemoOrg}" 
			serverurl="${sf.serverUrlDemoOrg}" 
			retrieveTarget="${sf.retrieveTargetDemoOrg}" 
			unpackaged="${sf.unpackaged}" />
	</target>
	
	These two jobs define how you will deploy to your Demo Org, and how you will retrieve metadata from it.
	
4. Copy and paste the following	over the ENTIRETY of build.properties:

sf.deployRoot_DemoOrg=C:/path/to/where/you/store/ant/DemoOrg/src

sf.usernameDemoOrg=username@example.com
sf.passwordDemoOrg=PASSWORDSECURITYTOKEN
sf.serverUrlDemoOrg=https://login.salesforce.com/
sf.retrieveTargetDemoOrg=DemoOrg/src

sf.unpackaged=package.xml

5. Navigate to where you store ant, and delete the "codepkg", "mypkg", "removecodepkg", and "unpackaged" directories.
6. Create a new folder structure that matches "sf.retrieveTargetDemoOrg" that you put in build.properties.
7. Clone the DevOps Interview Hub to your machine using: git clone git@bitbucket.org:acumensolutions/devops_interview_hub.git
8. Run the following command to see all of the available Scenarios to do: git branch -r

- From here on out, you'll choose a Scenario you want to do. You'll check out that branch and copy src/ AND package.xml to the folder you made in step 6.

- In order to run ant, you'll run either of these commands from the ant folder itself:
	- ant build_DemoOrg
	- ant retrieve_DemoOrg

- This folder should contain the following:
	- The directories you created in Step 6
	- build.properties
	- build.xml
	
- You should always start by attempting to deploy the codebase AS IS from Git. This will give you the errors you need to solve. Once you're ready to test your fixes, simply re-run the deploy command. You'll either get a Deployment Succeeded message, or a new list of build errors.
- Once you clear out all of the build errors for a certain Scenario, you can move onto the next one.
