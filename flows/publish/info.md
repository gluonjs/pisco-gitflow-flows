# Flow publish

1. [Description](#description)
1. [Steps](#steps)
1. [Excluded Contexts](#excluded-contexts)

## <a nmae="description"></a>Description

Publish generated artifact

## <a nmae="steps"></a>Steps

```json
{
  "publish": {}
}
```

* `publish`: All commands needed to upload an artifact to any artifacts repository for the contexts this artifacts are going to be used by upwards dependencies.
    
We can configure to publish a node library in [npmjs][8], or in [artifactory][9], or a maven library in a [Nexus][10] repository, etc...

## <a nmae="excluded-contexts"></a>Excluded contexts

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
[8]: https://www.npmjs.com/
[9]: https://www.jfrog.com/open-source/
[10]: https://www.sonatype.com/nexus-repository-sonatype
