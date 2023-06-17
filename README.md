# TCL_WORKSHOP_SANJANA
## DAY1
### Code
```tcl
#!/bin/tcsh -f
echo " This is a TCL file created by sanjana "

set my_work_dir = `pwd`

#------------------------------------------------------------------------
#---------------------------TOOL INITIALIZATION--------------------------
#------------------------------------------------------------------------


if ($#argv != 1) then
	echo " Info: Please provide a csv file "
	exit 1
endif

if (! -f $argv[1] || $argv[1] == "-help")then
	if ($argv[1] != "-help")then
		echo "ERROR: Could not find the file $argv[1]. Exiting..."
		exit 1
	else
		echo "User Manual will be printed on how to use this tool"
		exit 1
	endif
else
	tclsh vsdsynth.tcl $argv[1]
endif
```
### Output

<img width="553" alt="image" src="https://github.com/SanjanaHoskote/TCL_WORKSHOP_SANJANA/assets/128903809/dc8c4e88-007f-44e6-9155-bae5ee71f9c0">

## DAY2 

### Code
```tcl
#! /bin/env tclsh

#-----------------------------------------------------------#
#----- Checks whether panda usage is correct or not -----#
#-----------------------------------------------------------#

set generate_sdc 1
set enable_prelayout_timing 1
set working_dir [exec pwd]
set pan_array_length [llength [split [lindex $argv 0] .]]
set input [lindex [split [lindex $argv 0] .] $pan_array_length-1]

if {![regexp {^csv} $input] || $argc!=1 } {
puts "Error in usage"
puts "Usage: ./panda <.csv>"
puts "where <.csv> file has below inputs"
exit
} else {
#-----------------------------------------------------------------------------------------------------------------------------------------------------#
#------ converts .csv to matrix and creates initial variables "DesignName OutputDirectory NetlistDirectory EarlyLibraryPath LateLibraryPath"----------#
#----------- If you are modifying this script, please use above variables as starting point. Use "puts" command to report above variables-------------#
#-----------------------------------------------------------------------------------------------------------------------------------------------------#
        set filename [lindex $argv 0]
        package require csv
        package require struct::matrix
        struct::matrix m
        set f [open $filename]
        csv::read2matrix $f m , auto
        close $f
        set columns [m columns]
        m add columns $columns
        m link my_arr
        set num_of_rows [m rows]
        set i 0
        while {$i < $num_of_rows} {
                 puts "\nInfo: Setting $my_arr(0,$i) as '$my_arr(1,$i)'"
                 if {$i == 0} {
                         set [string map {" " ""} $my_arr(0,$i)] $my_arr(1,$i)
                 } else {
                         set [string map {" " ""} $my_arr(0,$i)] [file normalize $my_arr(1,$i)]
                 }
                  set i [expr {$i+1}]
        }
}

puts "\nInfo: Below are the list of initial variables and their values. User can use these variables for further debug. Use 'puts <variable name>' command to query value of below variables"
puts "DesignName = $DesignName"
puts "OutputDirectory = $OutputDirectory"
puts "NetlistDirectory = $NetlistDirectory"
puts "EarlyLibraryPath = $EarlyLibraryPath"
#------------------------------------------------------------------------------------------------------------------------------------------------------#
#---------------------------------------To check if directories and files in .csv file are valid-------------------------------------------------------#
#------------------------------------------------------------------------------------------------------------------------------------------------------#

if {![file isdirectory $OutputDirectory]} {
        puts "\n Info: Couln't find output directory in the path $OutputDirectory. Creating it.."
        file mkdir $OutputDirectory
} else {
        puts "\n Found output directory in the path $OutputDirectory"
}

if {! [file exists $EarlyLibraryPath] } {
        puts "\nError: Cannot find early cell library in path $EarlyLibraryPath. Exiting... "
        exit
} else {
        puts "\nInfo: Early cell library found in path $EarlyLibraryPath"
}


if {! [file exists $LateLibraryPath]} {
        puts "\nError: Cannot find late cell library in path $LateLibraryPath. Exiting... "
        exit
} else {
        puts "\nInfo: Late cell library found in path $LateLibraryPath"
}

if {! [file isdirectory $NetlistDirectory]} {
        puts "\nError: Cannot find RTL netlist directory in path $NetlistDirectory. Exiting..."
        exit
} else {
        puts "\nInfo: RTL netlist directory found in path $NetlistDirectory"
}

if {! [file exists $ConstraintsFile] } {
        puts "\nError: Cannot find constraints file in path $ConstraintsFile. Exiting... "
        exit
} else {
        puts "\nInfo: Constraints file found in path $ConstraintsFile"
}


#Constraints file creation
#SDC format
puts "\nInfo: Dumping SDC constraints for $DesignName"
::struct::matrix constraints
set chan [open $ConstraintsFile]
csv::read2matrix $chan constraints , auto
close $chan
set number_of_rows [constraints rows]
puts "number_of_rows = $number_of_rows"
 #------------------------------------------------------------------------------------------------------------------------------------------------------#
#---------------------------------------To check if directories and files in .csv file are valid-------------------------------------------------------#
#------------------------------------------------------------------------------------------------------------------------------------------------------#

if {![file isdirectory $OutputDirectory]} {
        puts "\n Info: Couln't find output directory in the path $OutputDirectory. Creating it.."
        file mkdir $OutputDirectory
} else {
        puts "\n Found output directory in the path $OutputDirectory"
}

if {! [file exists $EarlyLibraryPath] } {
        puts "\nError: Cannot find early cell library in path $EarlyLibraryPath. Exiting... "
        exit
} else {
        puts "\nInfo: Early cell library found in path $EarlyLibraryPath"
}


if {! [file exists $LateLibraryPath]} {
        puts "\nError: Cannot find late cell library in path $LateLibraryPath. Exiting... "
        exit
} else {
        puts "\nInfo: Late cell library found in path $LateLibraryPath"
}

if {! [file isdirectory $NetlistDirectory]} {
        puts "\nError: Cannot find RTL netlist directory in path $NetlistDirectory. Exiting..."
        exit
} else {
        puts "\nInfo: RTL netlist directory found in path $NetlistDirectory"
}

if {! [file exists $ConstraintsFile] } {
        puts "\nError: Cannot find constraints file in path $ConstraintsFile. Exiting... "
        exit
} else {
        puts "\nInfo: Constraints file found in path $ConstraintsFile"
}


#Constraints file creation
#SDC format
puts "\nInfo: Dumping SDC constraints for $DesignName"
::struct::matrix constraints
set chan [open $ConstraintsFile]
csv::read2matrix $chan constraints , auto
close $chan
set number_of_rows [constraints rows]
puts "number_of_rows = $number_of_rows"
 #------------------------------------------------------------------------------------------------------------------------------------------------------#
#---------------------------------------To check if directories and files in .csv file are valid-------------------------------------------------------#
#------------------------------------------------------------------------------------------------------------------------------------------------------#

if {![file isdirectory $OutputDirectory]} {
        puts "\n Info: Couln't find output directory in the path $OutputDirectory. Creating it.."
        file mkdir $OutputDirectory
} else {
        puts "\n Found output directory in the path $OutputDirectory"
}

if {! [file exists $EarlyLibraryPath] } {
        puts "\nError: Cannot find early cell library in path $EarlyLibraryPath. Exiting... "
        exit
} else {
        puts "\nInfo: Early cell library found in path $EarlyLibraryPath"
}


if {! [file exists $LateLibraryPath]} {
        puts "\nError: Cannot find late cell library in path $LateLibraryPath. Exiting... "
        exit
} else {
        puts "\nInfo: Late cell library found in path $LateLibraryPath"
}

if {! [file isdirectory $NetlistDirectory]} {
        puts "\nError: Cannot find RTL netlist directory in path $NetlistDirectory. Exiting..."
        exit
} else {
        puts "\nInfo: RTL netlist directory found in path $NetlistDirectory"
}

if {! [file exists $ConstraintsFile] } {
        puts "\nError: Cannot find constraints file in path $ConstraintsFile. Exiting... "
        exit
} else {
        puts "\nInfo: Constraints file found in path $ConstraintsFile"
}


#Constraints file creation
#SDC format
puts "\nInfo: Dumping SDC constraints for $DesignName"
::struct::matrix constraints
set chan [open $ConstraintsFile]
csv::read2matrix $chan constraints , auto
close $chan
set number_of_rows [constraints rows]
puts "number_of_rows = $number_of_rows"
set clock_start [lindex [lindex [constraints search all CLOCKS] 0 ] 1]
puts "clock_start = $clock_start"
set clock_start_column [lindex [lindex [constraints search all CLOCKS] 0 ] 0]
puts "clock_start_column = $clock_start_column"

#set clock_period [constraints get cell [expr {$clock_start+1}] [expr {$clock_start_column+1}]]

#-----check row number for "inputs" section in constraints.csv---##
set input_ports_start [lindex [lindex [constraints search all INPUTS] 0 ] 1]
puts "input_ports_start = $input_ports_start"


#-----check row number for "outputs" section in constraints.csv---##
set output_ports_start [lindex [lindex [constraints search all OUTPUTS] 0 ] 1]
puts "output_ports_start = $output_ports_start"
```
### Output
  <img width="852" alt="image" src="https://github.com/SanjanaHoskote/TCL_WORKSHOP_SANJANA/assets/128903809/36617733-4e4c-4420-9dcf-ae8363bb8d3b">
                                                                                                                                                                                                                                                                                                                                     
                                                                                                                                                                                              
