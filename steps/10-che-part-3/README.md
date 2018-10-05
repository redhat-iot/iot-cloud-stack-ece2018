# Start editing with Che

## Local editing

* Open the "Demo gauge" workspace
* Make some minor modification on the Web UI

## Edit startup configuration

  * In the navigator on the left, switch to the "Manage commands" tab
  * Double click on "buildAndRun"
  * Add the following content before the `npm start` line
    
        export KAFKA_PROJECT=kafka
        export PAYLOAD_FORMAT=kura
  * Press "Save"

## Starting locally

  * Click on the "play" button in the top of the view
  * Look for the "preview" link in the new "buildAndRun" terminal
  * Click on the preview link

You can now make some more modifications on the `index.html` file, reloading
the preview browser tab will immediately show the result.

## Commit and push

  * Commit and push the changes to the `tutorial-ece2018` branch
  * Switch to the "Demo Gauge" project in OKD
  * The build for application "hono-example-demo-gauge" should be running again
  * After the build is finished, check that the change are visible

## Troubleshooting

  * If the gauge doesn't show any data, try restarting the pod in the Kura application
