# Importing projects

## Import Kura Examples

  * Create a new workspace
    * Select the "Java CentOS" image, search in "Single Machine" category
    * Enter "kura-example" as a "Name" of the workspace
    * Do not add any projects!
    * Press "Create & Proceed editing" (in the dropdown list)
    * Press "Edit"
    * Switch to "Installers"
    * Enable "Git credentials"
    * Press "Save" (bottom of the page)
    * Press "Open" (top of the page)
  * Configure workspace
    * Open "Profile" -> "Preferences"
    * Switch to "Git / Committer"
      * Enter name and e-mail
    * Switch to "SSH / VCS"
      * Press "Generate Key"
      * Enter `github.com`
      * Press "View" in column "Public Key"
      * Copy "Public SSH Key"
      * Add the key to your GitHub account
  * Import project
    * Select "Import project…"
    * Use "Git" (not "Git Hub")
      * URL: git@github.com:&lt;you&gt;/kura-examples.git
      * Enable "Import recursively"
      * Tick the checkbox on "Branch"
      * And enter the following branch: `tutorial-ece2018`
      * Press "Import"
    * In the project configuration dialog which pops up
      * Select "Java / Maven"
      * Press "Save"

## Import projects via factories

Create new workspaces by opening the following links:

  * https://che-che.[[cluster00]].amazing.iot-playground.org/f?url=https://github.com/ctron/hono-example-bridge/tree/tutorial-ece2018
  * https://che-che.[[cluster00]].amazing.iot-playground.org/f?url=https://github.com/ctron/hono-example-demo-gauge/tree/tutorial-ece2018

After the import completed, you need to reset the "Git remote" to your forked location, using SSH instead of HTTPS and also switch to the branch `tutorial-ece2018`:

  * Open "Git" -> "Remotes…" -> "Remotes…"
    * Delete the existing "origin" remote
    * Add a new remote named "origin" in the form of: `git@github.com:<you>/<project>.git`
    * Press "Close"
  * Open "Git" -> "Remotes…" -> "Fetch"
    * Press "Fetch"
  * Open "Git" -> "Branches…"
    * Select `origin/tutorial-ece2018`
    * Click on "Checkout"

## Create GitHub webhooks

You can find out the GitHub webhook settings for each OKD project using the following steps.

### Getting webhook information from OKD

Switch to the project:

    oc project <project>

Get all build configurations:

    oc get bc

Which should give a list like:

    NAME                      TYPE      FROM      LATEST
    hono-example-demo-gauge   Source    Git       1

Then get the web hook settings:

    oc describe bc hono-example-demo-gauge

Look for the section "Webhook GitHub":

    …
    Webhook GitHub:
    	URL:	https://[[cluster00]].amazing.iot-playground.org:8443/apis/build.openshift.io/v1/namespaces/demo-gauge/buildconfigs/hono-example-demo-gauge/webhooks/<secret>/github
    …

And extract the GitHub webhook secret, use the output of this command to replace the `<secret>` placeholder above:

    oc get bc hono-example-demo-gauge -o jsonpath --template '{..github.secret}'

### Setting a build trigger

** This step is optional! Don't do it if the trigger already exists **

If a build configuration is missing a build trigger, a new one can be added with the following command:

    oc set triggers  bc <build-config> --from-github

### Adding webhooks in GitHub

For each build configuration (kura-app-generator-1, hono-example-demo-gauge, hono-example-bridge):

  * Extract the webhook information as described above 
  * Go to your GitHub project fork
  * Switch to "Settings" -> "Webhooks"
  * Click on "Add webhook"
    * Enter the Payload URL
    * Set the "Content Type" to `application/json`
    * Leave the "secret" empty
    * Leave the SSL verification enabled
    * Press "Add webhook"
  * Verify the webhook by opening it again and check the log at the bottom of the page
