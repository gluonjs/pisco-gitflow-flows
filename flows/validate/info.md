# Flow Validate: Standard validation pipeline

1. [Description](#description)
1. [Steps](#steps)
1. [Excluded Contexts](#excluded-contexts)

## <a name="description"></a>Description

This is the main flow for Continuous Integration. 
It has defined several steps needed for almost every software
context (maven library, cells app, gradle library, J2EE web application, etc...).

## <a name="steps"></a>Steps

The steps of the flow are the following. 
The definition of the flow is in the [config.json][8] file.

```json
{
  "provide": {
    "type": "flow"
  },
  "build": {
    "type": "flow"
  },
  "check": {
    "type": "flow"
  }, 
  "package": {
    "type": "flow"
  },
  "publish": {
    "type": "flow"
  },
  "deploy": {
    "type": "flow"
  },
  "test": {
    "type": "flow"
  }
}
```

#### Flow [provide][a]

Provide and install all dependencies and requirements.

* Steps

    ```json
      {
        "provide-env": {
          "implementation-check" : false
        },
        "configure-env": {
          "implementation-check" : false
        },
        "check-install": {
          "implementation-check" : false
        }
      }
    ```

    * `provide-env`: Execute all commands necessary to provide an environment for the entire C.I. process.
    * `configure-env`: Execute all commands necessary to configure an environment for the entire C.I. process.
    * `check-install`: Checking that all the requirements over the system have been fulfilled.
    
    As defined, those are not steps required in order to execute correctly the flow.

#### Flow [build][b]

In this section we will build the software unit.
We will resolve all the software **dependencies** of the 
software and we will **compile** the code and detect all the 
compilation-time errors.

* Steps:

    ```json
    {
        "resolve-deps": {},
        "build": {}
    }
    ```
    
    * `resolve-deps`: Resolve all the dependencies in compilation time defined. Check for the bower.json dependencies, or the maven dependecies, or the package.json dependencies. Provide all dependencies necessary to build the source code of the context.
    * `build`: Compile, apply templating, prepare source code for be tested, packaged and deployed.

#### Flow [check][c]

In this step, the flow validate will check all the qualities of the software unit than can be measured without any deploy of the software unit.
For example we can measure the bugs in the code, run the unit tests and check for the coverage, ...

* Steps:

    ```json
    {    
      "unit-testing": {
        "implementation-check" : false
      },
      "static-analysis": {
        "type" : "flow"
      },
      "structural-testing": {
        "type" : "flow"
      }
    }


#### Flow [package][d]

The validate flow will generate the **artifact** software for this software unit. Usually it involves compress the result of the build process, but it depends on the **build tool** that we have used for our software unit.

* Steps:

    ```json
    {
      "package": {}
    }
    ```
    

#### Flow [publish][e]

The validate flow will publish (as configured) the artifacts generated in the previous package step.

* Steps:

    ```json
    {
      "publish": {}
    }
    ```
    
    We can configure to publish a node library in [npmjs][9], or in [artifactory][10], or a maven library in a [Nexus][11] repository, etc...


#### Flow [deploy][f]

Once the software has been packaged and published in the correspondent platform, we have to deploy it in order to be able to test this particular artifact in his environment.

The particular environment will be calculated in function of several parameters:

* `branch type`: develop, master, feature, hotfix, etc...
* `configuration`: the configuration of the deploy itself.
* `stage in the CI process`: development, preproduction, UAT, production, ...

#### Flow [test][g]

In this step of the flow we have to test the behaviour of the software unit once it has been deployed in the specific environment.
In order to do so, this step has an input from the deploy step so the tests
are executed against the correct platform and artifact.

We have several types of tests in this stage, and we have defined them as steps of this flow:

* Steps:

    ```json
    {
        "smoke-testing": {
          "implementation-check" : false
        },
        "functional-testing": {
          "implementation-check" : false
        },
        "performance-testing": {
          "implementation-check" : false
        },
        "security-testing": {
          "implementation-check" : false
        },
        "usability-testing": {
          "implementation-check" : false
        },
        "acceptance-tests": {
          "type" : "flow"
        }
    }


## <a name="excluded-contexts"></a>Excluded contexts

All the gitflow contexts are excluded:

* [develop][1]
* [master][2]
* [feature][3]
* [hotfix][4]
* [release][5]
* [merger][6]
* [consolidation][7]

[1]: https://github.com/cellsjs/pisco-gitflow-contexts/blob/master/contexts/develop/index.js
[2]: https://github.com/cellsjs/pisco-gitflow-contexts/blob/master/contexts/master/index.js
[3]: https://github.com/cellsjs/pisco-gitflow-contexts/blob/master/contexts/feature/index.js
[4]: https://github.com/cellsjs/pisco-gitflow-contexts/blob/master/contexts/hotfix/index.js
[5]: https://github.com/cellsjs/pisco-gitflow-contexts/blob/master/contexts/release/index.js
[6]: https://github.com/cellsjs/pisco-gitflow-contexts/blob/master/contexts/merger/index.js
[7]: https://github.com/cellsjs/pisco-gitflow-contexts/blob/master/contexts/consolidation/index.js
[8]: ./config.json
[9]: https://www.npmjs.com/
[10]: https://www.jfrog.com/open-source/
[11]: https://www.sonatype.com/nexus-repository-sonatype
[a]: ../provide/info.md
[b]: ../build/info.md
[c]: ../check/info.md
[d]: ../package/info.md
[e]: ../publish/info.md
[f]: ../deploy/info.md
[g]: ../test/info.md
