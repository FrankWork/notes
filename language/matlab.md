help
帮助主题:

matlab/matfun                  - Matrix functions - numerical linear algebra.
matlab/datatypes               - Data types and structures.
matlab/timefun                 - Time and dates.
matlab/elfun                   - Elementary math functions.
matlab/general                 - General purpose commands.
matlab/funfun                  - Function functions and ODE solvers.
matlab/sparfun                 - Sparse matrices.
matlab/ops                     - Operators and special characters.
matlab/polyfun                 - Interpolation and polynomials.
matlab/randfun                 - Random matrices and random streams.
matlab/datafun                 - Data analysis and Fourier transforms.
matlab/iofun                   - File input and output.
matlab/specfun                 - Specialized math functions.
matlab/strfun                  - Character arrays and strings.
matlab/lang                    - Programming language constructs.
matlab/elmat                   - Elementary matrices and matrix manipulation.
matlab/datastoreio             - (没有目录文件)
matlab/datamanager             - (没有目录文件)
matlab/guide                   - Graphical user interface design environment
testframework/core             - (没有目录文件)
matlab/bigdata                 - (没有目录文件)
matlab/codetools               - Commands for creating and debugging code
matlab/graphfun                - (没有目录文件)
testframework/performance      - (没有目录文件)
hardware/stubs                 - (没有目录文件)
matlab/optimfun                - Optimization and root finding.
matlab/verctrl                 - Version control.
matlab/helptools               - Help commands.
matlab/images                  - (没有目录文件)
matlab/demos                   - Examples.
toolbox/local                  - General preferences and configuration information.
matlab/winfun                  - Windows Operating System Interface Files (COM/DDE)
winfun/NET                     - Using .NET from within MATLAB
matlab/mapreduceio             - (没有目录文件)
matlab/graph2d                 - Two dimensional graphs.
matlab/graph3d                 - Three dimensional graphs.
matlab/graphics                - Handle Graphics.
graphics/obsolete              - (没有目录文件)
matlab/plottools               - Graphical plot editing tools 
matlab/scribe                  - Annotation and Plot Editing.
scribe/obsolete                - (没有目录文件)
matlab/specgraph               - Specialized graphs.
matlab/uitools                 - Graphical user interface components and tools
uitools/obsolete               - (没有目录文件)
matlab/serial                  - (没有目录文件)
uicomponents/uicomponents      - (没有目录文件)
uicomponents/graphics          - (没有目录文件)
controllib/general             - Control System Toolbox -- General Utilities.
shared/rptgen                  - (没有目录文件)
stats/mlearnapp                - Statistics and Machine Learning Toolbox
stats/gpu                      - (没有目录文件)
shared/statslib                - Statistics and Machine Learning Toolbox Library
shared/dastudio                - (没有目录文件)
webservices/restful            - (没有目录文件)
interfaces/webservices         - MATLAB Web Services Interfaces.
matlab/apps                    - (没有目录文件)
stats/stats                    - Statistics and Machine Learning Toolbox
stats/classreg                 - (没有目录文件)
stats/clustering               - (没有目录文件)
stats/bayesoptim               - (没有目录文件)
matlab/imagesci                - (没有目录文件)
shared/instrument              - (没有目录文件)
matlab/audiovideo              - Audio and Video support.
matlab/networklib              - Network support.
uicomponents/components        - (没有目录文件)
optim/optimdemos               - Demonstrations.
controllib/graphics            - Control Library - Graphics.
graphics/utils                 - (没有目录文件)
graphics/plotoptions           - (没有目录文件)
hdllib/ml_lib                  - (没有目录文件)
shared/optimlib                - Optimization Toolbox Library
shared/comparisons             - (没有目录文件)
matlab/timeseries              - Time series data visualization and exploration.
matlab/hds                     - (没有目录文件)
shared/m3i                     - (没有目录文件)
interfaces/json                - (没有目录文件)
interfaces/python              - (没有目录文件)
appdesigner/appdesigner        - (没有目录文件)
shared/io                      - (没有目录文件)
matlab/toolbox_packaging       - (没有目录文件)
connector/connector            - connector  Enable or disable the MATLAB Connector. The MATLAB Connector allows you to access a MATLAB session on a desktop from a mobile device using MATLAB Mobile.
stats/statsdemos               - (没有目录文件)
optim/optim                    - Optimization Toolbox
matlab/webcam                  - Webcam support.
stats/bigdata                  - (没有目录文件)

  General purpose commands.
  MATLAB Version 9.1 (R2016b) 25-Aug-2016 
 
  General information.
    syntax        - Help on MATLAB command syntax.
    demo          - Run demonstrations.
    ver           - MATLAB, Simulink and toolbox version information.
    version       - MATLAB version information.
    verLessThan   - Compare version of toolbox to specified version string.
    logo          - Plot the L-shaped membrane logo with MATLAB lighting.
    membrane      - Generates the MATLAB logo.
    bench         - MATLAB Benchmark.
  
  Managing the workspace.
    who           - List current variables.
    whos          - List current variables, long form. 
    clear         - Clear variables and functions from memory.
    onCleanup     - Specify cleanup work to be done on function completion.
    pack          - Consolidate workspace memory.
    load          - Load workspace variables from disk.
    save          - Save workspace variables to disk. 
    saveas        - Save Figure or model to desired output format.
    memory        - Help for memory limitations.
    recycle       - Set option to move deleted files to recycle folder.
    quit          - Quit MATLAB session.
    exit          - Exit from MATLAB.
 
  Managing commands and functions.
    what          - List MATLAB-specific files in directory.
    type          - Display MATLAB program file.
    open          - Open files by extension.
    which         - Locate functions and files.
    pcode         - Create pre-parsed pseudo-code file (P-file).
    mex           - Compile MEX-function. 
    inmem         - List functions in memory. 
    namelengthmax - Maximum length of MATLAB function or variable name.
 
  Managing the search path.
    path          - Get/set search path.
    addpath       - Add directory to search path.
    rmpath        - Remove directory from search path.
    rehash        - Refresh function and file system caches.
    import        - Import packages into the current scope.
    finfo         - Identify file type against standard file handlers on path.
    genpath       - Generate recursive toolbox path.
    savepath      - Save the current MATLAB path in the pathdef.m file.
 
  Managing the java search path.
    javaaddpath   - Add directories to the dynamic java path.
    javaclasspath - Get and set java path.
    javarmpath    - Remove directory from dynamic java path.
 
  Controlling the command window.
    echo          - Display statements during function execution.
    more          - Control paged output in command window.
    diary         - Save text of MATLAB session.
    format        - Set output format.
    beep          - Produce beep sound.
    desktop       - Start and query the MATLAB Desktop.
    preferences   - Bring up MATLAB user settable preferences dialog.
 
  Operating system commands.
    cd            - Change current working directory.
    copyfile      - Copy file or directory.
    movefile      - Move file or directory.
    delete        - Delete file or graphics object.
    pwd           - Show (print) current working directory.
    dir           - List directory.
    ls            - List directory.
    fileattrib    - Set or get attributes of files and directories.
    isdir         - True if argument is a directory.
    mkdir         - Make new directory.
    rmdir         - Remove directory.
    getenv        - Get environment variable.
    !             - Execute operating system command (see PUNCT).
    dos           - Execute DOS command and return result.
    unix          - Execute UNIX command and return result.
    system        - Execute system command and return result.
    perl          - Execute Perl command and return the result.
    computer      - Computer type.
    isunix        - True for the UNIX version of MATLAB.
    ispc          - True for the PC (Windows) version of MATLAB.
 
  Debugging.
    debug         - List debugging commands.
 
  Tools to locate dependent functions of a program file.
    depfun        - Locate dependent functions of program file.
    depdir        - Locate dependent directories of program file.
 
  Loading and calling shared libraries.
    calllib          - Call a function in an external library.
    libpointer       - Creates a pointer object for use with external libraries.
    libstruct        - Creates a structure pointer for use with external libraries.
    libisloaded      - True if the specified shared library is loaded.
    loadlibrary      - Load a shared library into MATLAB. 
    libfunctions     - Return information on functions in an external library.
    libfunctionsview - View the functions in an external library.
    unloadlibrary    - Unload a shared library loaded with LOADLIBRARY.
    java             - Using Java from within MATLAB.
    usejava          - True if the specified Java feature is supported in MATLAB.
 
  See also lang, datatypes, iofun, graphics, ops, strfun, timefun, 
  matfun, demos, graphics, datafun, uitools, doc, punct, arith.
