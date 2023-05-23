# my-phd-faq-notes

### Specific to Cambridge
<details>
<summary>Backup</summary>
- theory-fs-nethome is an expensive high-reliability storage and it is mounted on our workstation in ~/theory-fs-nethome/<br>
- If you cannot see your stuff in theory-fs-nethome and you did not remove it, there maybe a network problem<br>
- If you still cannot see it after network problem is resolved, just log back off and log back in (with a password, not an ssh key)<br>
- You can often access the most recent backup of a machine under /rsnapshots but not always<br>
- The latest data about backups are available from a monitoring system at https://hobbit.ch.cam.ac.uk<br>
- On the above website, search for your machine, click on backup and/or backuploc dot<br>
- Usually we keep the backups in two or more physically separated places<br>
- scp and rsync (use of dir vs dir/)<br>
</details>
<details>
<summary>Clusters/Workstation</summary>
- /home is backed up, /scratch and /sharedscratch are not backed up<br>
- /scratch2 is on SSD (fast, less space) and /scratch is on conventional hard drive.<br>
- nest and wales02 run on different operating systems, CentOS and Ubuntu respectively.<br>
- Software should be built and reconfigured for each operating system as different operating systems are not binary compatible.<br>
- We usually use gcc (gfortran) and intel (ifort) compilers, not pgi compilers.<br>
</details>
<details>
<summary>Working remotely</summary>
- [Remote working tools](https://www.ch.cam.ac.uk/computing/remote-working-tools)<br>
- For running linux on a windows machine, use either virtual box or dual boot<br>
- Remote login either via citadel or VPN.<br>
- Use ssh-keygen to store a key so that you do not have to supply password every time.<br>
- To use sshfs you will want to connect via VPN.<br>

</details>
<details>
<summary>Managed Linux workstations</summary>
- [Managed linux workstation faq](https://www.ch.cam.ac.uk/computing/managed-linux-workstations-faq) <br>
- [Software available on linux workstation](https://www.ch.cam.ac.uk/computing/ubuntu-1804-managed-linux-workstation-software)<br>
</details>

### Common problems
<details>
<summary>SSH</summary>
- 'ssh: connect ... port 22: No route to host': due to network problem. Try to reboot the machine that you are trying to connect to. <br>
- In general, just try to reboot if possible.<br>
- ssh -X is used to ssh with X-forwarding.<br>
</details>
<details>
<summary>Local workstation</summary>
- 'System voltage low': could be caused by a small motherboard failing. Email computer officers.<br>
- 'No Bluetooth Found. Plug in dongle to use Bluetooth': You need USBBT1EDR4. <br>
- Local workstation is hanged: Try to ssh into your workstation from a different computer and do `sudo reboot`<br>
</details>
<details>
<summary>Printer</summary>
- Printer is not printing pdfs: try to print a simple text file (not .pdf, .ps, .odt) using 
`lpr -P printername filename` <br>
- In general, try to do power off and then power on.<br>
</details>
<details>
<summary>Libraries and modules</summary>
- libgfortran.so.5: cannot open shared libraries<br>
- When a software is built using a set of compilers, you need the same compilers (via libraries) to be found at the runtime.<br>
- The libaries can be found by loading the module or by setting the `LD_LIBRARY_PATH`, `LIBRARY_PATH` and/or `LD_RUN_PATH`.<br>
- Loading module tells the linker to add the right directories to binary's library search path when you build a binary.<br>
- readelf -d somebinary, to see the library search path built into a binary<br>
- -L, -Wl,-rpath<br>
- rpm -qa | grep packagename, to check the installed package<br>
- rpm -ql exactpackagename, to check the installation location of the package.<br>
- If you want your build process to look at a particular location for the installed package, use `-Dpackagename_INCLUDE_DIR=/location/exactpackage`<br>
- If there are errors while loading shared libraries, find the missing library and add the directory to your `LD_LIBRARY_PATH`, maybe in your ~/.bashrc<br>
- `export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/pathto/newlibrary`<br>
- export is used if you want child processes to see the variable.<br>
- source ~/.bashrc<br>
- Executable maybe found in bin directory<br>
- MPI library just handles communication between processes, so its version should not affect numerical results.<br>
- Version of compilers and maths libraries should not make a significant difference to numerical results.<br>
- If it does make a difference it is because the code is buggy or the compiler is buggy.<br>
- Newer compilers are faster and hence preferred.<br>
- You can install softwares in your home and sharedscratch directories on cluster. /home/$USER/opt/ would be the normal choice of location.<br>
</details>
<details>
<summary>Tmux</summary>
- How to remotely run a long interactive job on your local workstation?<br>
- You want to shut down your laptop but do not want to log out from your local workstation.<br>
- I usually use it when I want to run rsync and scp for huge directories remotely.<br>
- tmux is used to create a session that you can attach/detach/reattach from.<br>
- You can start a session at one place and reattach to it from another. You can leave commands running in a session.<br>
- The session will persist until next reboot or until you end it yourself.<br>

</details>
<details>
<summary>Debugging MPI with GDB</summary>
- GDB is a GNU debugger<br>
- mpirun -np 2 xterm -e gdb /pathto/executable<br>
- run, p to print value of a variable, where, n<br>
- bt to get a backtrace.<br>
- Debug executable built using `-DCMAKE_BUILD_TYPE=Debug` flag<br>
- -fbacktrace -fbounds-check -ffpe-trap=zero,denormal<br>
- If you want to debug MPI code on nest, log into nest with X-forwarding on (ssh -X) on two different windows/terminals (opened using Ctrl+Alt+T).<br>
- Run xterm to see if it is working on both. To exit from xterm window just type exit in the xterm.<br>
- In terminal 1, start an interactive test job using<br>
- srun -n2 -pTEST --pty -u /bin/bash, if you want to use 2 CPUs on TEST node.<br>
- Leave that open and switch to terminal 2 and log into node-0-0 with X-forwarding by doing this<br>
- ssh -X node-0-0<br>
- Load the required modules, run debug command (from terminal 2) and the xterm should pop up on your desktop.<br>
- First try interactive debugging on local workstation. On cluster you will have to deal with workload manager complication.<br>
- Try to debug using different debug executables made using different compilers, run gdb on different machines (local workstation and clusters)<br>
- You will need to load the module for gdb on cluster.<br>
</details>

### Visualisation software specific problems
<details>
<summary>Pymol</summary>
- Currently, you need to unload anaconda to use pymol from command line.<br>
- Starting pymol by clicking its icon is different from opening it using command line.<br>
- Ray trace and get high resolution image (dpi=300)<br>
- Need to put useful command with examples<br>
</details>
<details>
<summary>VMD</summary>
- ERROR) Could not create OpenGL rendering context: Try reboot (possibly due to graphics driver update and mismatch)<br>
</details>
<details>
<summary>GIMP</summary>
- Can be used to do cropping easily<br>
</details>
<details>
<summary>Making xyz file</summary>
- You need x, y, z coordinates.<br>
- You can define atom labels in column 1.<br>
- The first line in the file contains the total number of atoms/particles/sites in your system.<br>
- The second line contains a comment.<br>
- From third line onwards, you have 4 columns, first: atom label, second, third and fourth correspond to x, y and z coordinates.<br>
</details>
<details>
<summary>Matlab</summary>
f1=(@(x,y) sin(x)+cos(y))<br>
H=fsurf(f1,[-10 10 -12 10],'ShowContours','on')<br>
%mycolors = [1 0 0; 0 1 0; 0 0 1];colormap("turbo");set(findobj(gcf, 'type','axes'), 'Visible','off')hold on;<br>

You might be able to see the plot when you open the file, but it is important to run it. Then you will be able to navigate over the plot and open it in the figure window. You can change the view and save it in whichever format you like.<br>

</details>
<details>
<summary>Gnuplot</summary>
- In the file my.plt write the following<br>
- `set terminal pdf`<br>
- `plot "Cv.out" using 1:2`<br>
- From the command line run, `gnuplot my.plt > my.pdf`<br>
</details>


### Miscellaneous problems 
<details>
<summary>Miscellaneous</summary>
- Taking department computer home during pandemic was not a good idea.<br>
- Softwares (modules) are supplied to department computers via the department network.<br>
</details>
<details>
<summary>CMAKE</summary>
- Make sure your are on the right branch, building in a clean directory.<br>
- If `make -j12` does not work, try, `make VERBOSE=1` or `make` or just try building using ccmake.<br>
- You can sometimes rerun make directly if you just added a print statement to the code and not made substantial changes for testing/debugging purpose.<br>
</details>
<details>
<summary>Git</summary>
- `git reset --hard` to discard all your local changes.<br>
- gitlab projects normally have their continuous integration tests defined in .gitlab-ci.yml<br>
</details>
<details>
<summary>Memory leak problem</summary>
- Report: cluster, node, directory from which the job was submitted, slurm output<br>
- Perhaps, that node needs a reboot<br>
- High use of swap memory is a bad sign<br>
- VALGRIND is used with a debug executable if there is some memory leak problem because of a bug in the code.<br>
- You can use various tools in VALGRIND like, `valgrind --tool=memcheck --xtree-memory=full debugexecutablename`<br>
- kcachegrind can be used to view the call tree.<br>
- `valgrind --leak-check=full --show-leak-kinds=all -v debugexecutablename`<br>
</details>


### My notes
<details>
<summary>SLURM</summary>
- --exclude to exclude a particular node, in case that node has a memory leak.<br>
- load the compiler modules that were used to compile the code even when you are submitting a job<br>
- even though you do not need to compile the code, the compiler is required to tell the system where to find the libraries against which the compile code was linked during compilation.<br>
- you do not need to load cmake.<br>
- the modules are loaded before you invoke the compiled binary but after the magic commands that the job scheduler reads.<br>
- Always create a new file with a list of handy commands to refer to. Do not copy all the commands and comment them out as required. Keep it short and clear to avoid any confusion.<br>
- Increase memory allocation by putting a command in the header of your sbatch script, with `#SBATCH --mem=5000`. The value is in MB.<br>
- Link for SLURM resources on Group wiki.<br>
- sinfo -V
</details>
<details>
<summary>CONDA environment</summary>
</details>
<details>
<summary>Fortran</summary>
- Index 1 of dimension 1 of array above upper bound of zero: when trying to access first element of an empty array.<br>
- Fortran runtime error: Bad integer for item 1 in list input: an integer was expected but there is no integer there.<br>
- gfortran myfile.f -o program.exe<br>
</details>
<details>
<summary>Linux</summary>
- df -h shows sizes in human readable format.<br>
- which git<br>
- echo "$PATH" | tr : '\n' to see one path per line.<br>
- ls /usr/bin to list the executables<br>
- top<br>
- free<br>
- `grep -w "search_exact_word_only" *`<br>
- grep -i, grep -r<br>
- chmod 755<br>
- meld is better than diff to visualise the difference between two files<br>
- `history -d <number>`, if you accidentally typed your password as a command on a computer with shared history accessible to others, you would want to delete the command from the history.<br>
</details>
<details>
<summary>Vim</summary>
- `:%s/,\{36\}/&\r/g` and `:g/^$/d` to convert rst (coords.inpcrd file without first two lines here) to start file<br>
</details>
<details>
<summary>Latex</summary>
- During installation, you might need things like, texlive-publishers and texlive-latex-extra<br>
- When using \textwidth, note that the values should sum to 1 if you want the objects to be in the same line.<br>
- texcount to help count words in your latex document as per a set of rules.<br>
- \frontmatter, the purpose of having it is that contents within it are not included in table of contents.<br>
- \addcontentsline can be used to manually add entries to table of contents. Use with caution.<br>
- Latex Error! Package inputenc Error: Unicode character ..., one of the bib entries may have a non-ASCII characters, put them in Latex format.<br>
- Overfull hbox, does not usually matter. It means that things might be disappearing off the right of the page.<br>
- This is a standard file: locate physics.sty, /usr/share/texlive/texmf-dist/tex/latex/physics/physics.sty I don't think you have a complete latex installation? Anyway, you can just put this file in the current working directory and it should be found.<br>
- it is a minus sign, not a hyphen, so use maths mode<br>


</details>
<details>
<summary>Figures for publications</summary>
- Crop the whitespace around png images using `convert -trim` command.<br>
</details>

### Softwarewales specific problems
<details>
<summary>Softwarewales</summary>
- Debug executable is different from DEBUG keyword.<br>
- LJ38 is one of the quickest system to run when debugging a code.<br>
- The second argument of TRMIN in dinfo file (used with disconnectionDPS program) takes the total number of minima in the database.<br>
- the statements written in output file start with `subroutine_name>`<br>
- grep read output <br>
- `grep -i exchange output* | grep -i successful | sort -k 1 | uniq`
- `awk '{print NR, $1}' min.data | sort -k 2nr | awk '$2 > -10 {print $1}'`, in case you want to get minima numbers for unphysical stationary points from the database
- `grep "Lowest Minimum" output* `
- The way the dump file is written needs to match the way it is read back.<br>
- LPERMDIST turns on local permutational matching. It checks to see whether different minima with similar energies are actually permutational isomers of each other. It will, for example, treat the three rotations of a methyl group as the same mimimum.<br>
- Just continue to question everything!<br>
- make sure you look at the output carefully and check anything<br>
that doesn't look right. <br>
- Ctrl+F is very useful<br>
- Underflow warnings should not be a problem. Overflows would be another matter!<br>
- Check if you have all the input files when your calculation fails abruptly.<br>
- Make sure you look at the structures.<br>
- Keep/backup lowest files or GMIN.dump files from basin-hopping. <br>
- Do not change so many variables at the same time, try to have a good control over the variable you are varying.<br>
- Sometimes the bug in old code maybe resolved in the newer versions.<br>
</details>
