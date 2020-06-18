# WorkflowDir Setup

## Hello world!

1. Install WorkflowDir
2. Open up a command prompt of your choice! We're using bash.
3. Make a new folder, mkdir HelloFlowDir
4. cd HelloFlowDir
5. wfd init
  * This creats a new file! check it out, it's called .flowyrc
6. Open that file! (vim .flowyrc)
7. Place the following into .flowyrc

```bash
#!/bin/bash

mv $filepath ../HelloWorld.txt
```

8. You're done! Now any file you put into HelloFlowDir will get moved out of the folder and renamed HelloWorld.txt
