# PlotterCAM Automator workflow 

Optimize one or more svg files (e.g. from your favorite DTP app) with vpype and create gcode through an Automator workflow. Access it via context menu in macos Finder without Terminal.

The vpype pipeline is stored in the workflow file. If you use different pipelines, I’d suggest to use multiple workflows. 

The juicy-gcode config is stored centrally. If you need configs on a per project basis, you need to adjust the path to the yaml file in the workflow.


## Install:
- Move `PlotterCAM.workflow` to `~/Library/Services`, so that it is available in Finder. To customize/edit the workflow, just open it in Automator
- Have vpype installed pipx style as described in the [docs](https://vpype.readthedocs.io/en/latest/). If you installed it in a different location, you need to  change `~/.local/pipx/venvs/vpype/bin/vpype` in the workflow to where vpype resides on your system
- Have juicy-gcode executable on your system. Go to [the repo](https://github.com/domoszlai/juicy-gcode) and from there to the releases page. Download the binary and copy `juicy-gcode` to `/usr/local/bin/juicy-gcode`. (Maybe you have to do `chmod +x juicy-gcode` there)
- Create a `.juicy.yaml` file and put it in your home directory (Access it via `CMD + Shift + h` in Finder). See the juicy readme for an example. The leading dot of the yaml file hides it in Finder. To see/hide hidden files, use shortcut `CMD + Shift + .`
- Done

## Usage
- Higlight one or more svg files in Finder
- Open the context menu, go to Quick Actions and click on the workflow
- The workflow passes the highlighted file(s) to a shell script that runs vppype and writes `yourfile.tmp.svg`. It then runs juicy-gcode on the temporary svg(s) and writes `yourfile.nc`
- There is no output except the temporary svg and the nc file. If something goes wrong, Automator will throw an error
