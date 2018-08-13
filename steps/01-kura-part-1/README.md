# Eclipse Kura™ – IoT Gateway

Also see:

  * https://github.com/ctron/kura-emulator/tree/master/openshift
  * https://github.com/eclipse/kura

## Perform installation

    oc new-project kura --display-name 'Eclipse Kura'
    oc new-app --file=https://raw.githubusercontent.com/ctron/kura-emulator/tutorial-ece2018/openshift/kura-data-persistence.yml -p GIT_BRANCH=tutorial-ece2018
