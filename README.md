powershell day 1
___________________________________________________________________________________________________________________________________________________________________________________________________________________________________
command to ssh/ get the gui from the oposing machine 
xfreerdp /u:student /v:x.x.x.x -dynamic-resolution +glyph-cache +clipboard

called commandlets (VERB-NOUN)
ex: Start, Get, Set, 


commands
------------------------
Get-command (lists all commands) 
Get-verb (gets verbs) 
get-command -noun  (gets all nouns)  
get-process(gets a list of proeccess)    Ailus[ps, gps] 
get -eventlog -logname (gets logs) 
Get-childitem (directory listing)
Get-member(all member types of a command) 
((get-proccess)[44].kill() (kills a specific process by an index position) 
wtie-output <name> (doesnt)
write-host <name>writes accross piplelins 
(<command>).gettype()


variables
------------------------------------------
Get-variable
about_variable
get-childitem env: (environment variables) 
$_ (pipe variable, allows for each item that goes through the pipe) 
$ (sorts
? (true) 
$<something> (definds one) 
Get-variable <variable>
del variable:<variable> 
single quote = literal (what you type) 
double quote = whats in a variable

help 
------------------------------------------
update-help -force -erroraction silentlycontinue 
get-help <what command you want help with> -full (full page) -showwindow (opens a gui) -online (opens online) -examples
get-help *log* (anytging about a log) 


Alis 
--------------------------------------------
get-alias 
dir, ls ,Get-childitem -> getting a direcorty listing
set-alias <command> <what you want to do> 
Remove-item alias:<command> 



Exercise day 1) 
-------------------------------------------------------
#1 

    Ensure that you have the latest copy of help by updating your help system.
  Update-help -force -erroraction silentcontinue

    Which cmdlets deal with the viewing/manipulating of processes?
  get-process

    Display a list of services installed on your local computer.\
  get-service 

    What cmdlets are used to write or output objects or text to the screen?
  write-host  write-output 

    What cmdlets can be used to create, modify, list, and delete variables?
  get-varaiable or del variable 

    What cmdlet can be used, other than Get-Help, to find and list other cmdlets?
get-command 
    Find the cmdlet that is used to prompt the user for input.
  read-host 





#2 


    Display a list of running processes.
get-process 
    Display a list of all running processes that start with the letter "s".
get-process -name s* 
    Find the cmdlet and its purpose for the following aliases:

        gal = get alias 

        dir= get-childitem 

        echo= write-output 

        ? = where-object

        % = foreach-object

        ft = format-table

    Display a list of Windows Firewall Rules.
  get-netfirewallrule

    Create a new alias called "gh" for the cmdlet "Get-Help"
set-alias gh get-help





#3 


    Create a variable called "var1" that holds a random number between 25-50.
get-random -min 25 -max 50 
    Create a variable called "var2" that holds a random number between 1-10.
$var2 = 1
    Create a variable called "sum" that holds the sum of var1 and var2.
$sum = $var1 + $var2
    Create a variable called "sub" that holds the difference of var1 and var2.
$sub = $var1 - $var2 
    Create a variable called "prod" that holds the product of var1 and var2.
$prod = $var1 * $var2
    Create a variable called "quo" that holds the quotient of var1 and var2.
$quo = $var1 / $var2
    Replace the variables in text with their values in the following format:

        "var1" + "var2" = "sum"
"{0} + {1} = {2} " -f $var1, $var2, $sum
    Replace the variables in text with their values in the following format:

        "var1" - "var2" = "sub"
"{0} - {1} = {2} " -f $var1, $var2, $sub
    Replace the variables in text with their values in the following format:

        "var1" * "var2" = "prod"
"{0} * {1} = {2} " -f $var1, $var2, $prod

    Replace the variables in text with their values in the following format:

        "var1" / "var2" = "quo"
"{0} / {1} = {2} " -f $var1, $var2, $quo


Day 2
___________________________________________________________________________________________________________________________________________

commands
-----------------------------------------------------------------
run script block = invoke-command or & <name of script block> 
get-childitem | sort-object -property lenght -decending 
get-childitem | sort-object -property extention | ft -groupby extention 
get-proccess| group-object {$_.name.substring(0,1).toupper()} | foreach-object{($_.name + " ") *7; "==================="; $_.group} 
-autosize -wrap 
get-uniqe 
measure-object length 
compare-object 

$mytruck = new-object object 
add-member -membertype noteproperty -name color -value red -inputobject $mytruck 
add-member -me noteproperty -in $mytruck -na make -value ford 
add-member -inputobject $mytruck noteproperty model "f-150 raptor" 
$mytruck |add-member noteproperty cab supercrew

$mytruck | add-member scriptmethod park { "finding a spot" }

comparison operators 
-------------------------------------------------------------------------
-eq     |  -like 
-ne     |  -notlike
-le     |  -match (uses regex)
-ge     |  -contains 
-gt     |  -and
-lt     |  -or 

script block
--------------------------------------------------------------------------
$<name>={get-service | ft Name, status} 
(to call it) & $<name>


exercise Day 2 
----------------------------------------------------------
#1 


    Display the start time of the earliest and latest running processes
    
Get-Process | Where-Object{$_.name -ne "idle"} | Sort-Object -Property StartTime | Select-Object -First 1 -Last 1 -Property StartTime

    Identify a cmdlet that returns the current date and time then using this cmdlet and Select-object, display only the current day of the week

Get-Date | Select-Object -Property DayOfWeek

    Identify a cmdlet that displays a list of installed hotfixes.

Get-HotFix

    Extend the expression to sort the list by install date, and display only the install date and hotfix ID.

Get-HotFix | Select-Object -Property HotFixID, InstalledOn | sort -Property installedOn -Descending

    Extend the expression further, but this time sort by description, include description, hotfix ID, and install Date.
    
Get-HotFix | Select-Object -Property description, HotFixID, InstalledOn | sort -Property description





#2 


   

    Create a custom object that contains information about the host system using the following:


        Win32_ComputerSystem

        Win32_BIOS

        Win32_OperatingSystem

        Win32_LogicalDisk

    Use the cmdlet Get-WmiObject to obtain the needed information

	

Store the objects results into variables to be used in the custom object
	

The custom object will only contain properties not methods

The final output of this exercise should look like the following:
Endstate

ComputerName    : DESKTOP-5KJDVS2
OperatingSystem : Microsoft Windows 10 Pro
Version         : 10.0.17134
Manufacturer    : Dell Inc.
Disks           : {\\DESKTOP-                          5KJDVS2\root\cimv2:Win32_LogicalDisk.DeviceID="C:",
                  \\DESKTOP-5KJDVS2\root\cimv2:Win32_LogicalDisk.DeviceID="D:"}

$my = New-object object
To add member: $my | Add-Member NoteProperty ComputerSystem WIN-OPS   (plus more) 
to see it do: $my | fl * 



#3 


    Find and extract the model number from the provided lines of text. If there isn’t a model number then display to the user that a model number wasn’t found

    Check both lines for model numbers and report individually the line and model number if found.

Use the following variables for your script

$line1 = "Do you have model number: MT5437 for john.doe@sharklasers.com?"
$line2 = "What model number for john.doe@sharklasers.com?"

	
Exercise Criteria

    Must use at least ONE comparison operator

    Must use at least ONE If Condition OR Switch Statement

answer: 
$line1 = "Do you have model number: MT5437 for john.doe@sharklasers.com?"
$line2 = "What model number for john.doe@sharklasers.com?"
patern = '[A-Za-z] {2} \d{2,5'
$line1,$line2 | %{if($_ -match $patern ) {$Matches.values } else {'Model not found'} }





day 3 
------------------------------------------------------------------------------------------------------------------------------------------------------

loop commands initeration 
---------------------------------
$num = 1,2,3,4,5
$num | Foreach-object {$_ *2} 
$num | Foreach-object {$_.upper}
Get-process | select-object -first 10 | foreach {$_.name} | foreach-object {$_.toupper()}


(for each item) 
These are do the same
-------------------------
Foreach ($item in gci C:\ -recurse){$item.name} 
gci C:\ -recurse | foreach-object{$_.name}

diff foreach
--------------------------------
foreach($num in 1..5){$num *2} 
$team = "yes" , "no" 
foreach($teams in $team){"hahah $team"}




while statement
-------------------------
while(condition){
<codeblock>
} 

$num = 0 
while ($num -lt 3) {
$num
$num++
}


do{ 
$num
$num++
}while ($num -lt 3)


do {
<code block> 
}until(condition) 


for 
----------------------------------------
for(initialization; condition; increment)
{ 
<code block 
}

array (list of objects) 
------------------------------------
$x = get-proccess 
($x).gettype()
$x -is [arry]
$x.count (see the lines in an array) 
$array2 = "world", "hello", 5 , 10 ,(get-date)
$array3 = @()    (empty array) 
$array[1]   (calls an element) 
$array[3,5]   (displays only inex postions 3-5) 
$array[4..array.length]   (gives you a slice from where you started) 


jagged array   (an array with instances of other arrays within it) 
---------------------------------------------------------------------
$jaggedarray = "y", "E", (1,('hey', 'nahh'), 3 ), "huh" 
jaggedarray [3][0]    (gets the value 1) 
jaggedarray [3][0][1]   (gets the value nahh) 



multi dementional array
-----------------------------------
$hello = @(
	(1,2,3)
 	(4,5,6)
  	(7,8,9)
   )
$hello[0][1]    (gets the value 2) 


 foreach ( line in $hello){
 	if ($line[2] -eq 3){
  	write-output $line
   }
   }



hashtabel (dictionary ) 
--------------------------------------------

$mylist = @{first = "john ; last = "doe" ; mid = "bon" ; age = 35} 
$mylist.first
$mylist.key
$mylist.value
$mylist[key] = what you want to change it to 
$mylist.remove(key) 

regex 
---------------------------------------------
go to cyberchef has ipv4 regex and other prebuilds


stream manipulation 
---------------------------------------------
"a" (allows variables to be converted 
`"yes`" (` allows for you to show special caracters) 
`n  (new line)
`t  (tab) 
`b  (back space) 


$yes = @" 

(enter what you want)


"@ 


replace 
---------------------------------
"hello john' -replace "john ,world" 
'server1,server2,server3' -replace '[,]',';'
(ipconfig) -match 'IPv4'
'[         john        bon          doe]' -replace '\s+', ' ' 
"cat","dog" -join "|"


functions 
-------------------------------------------------
function <name> {
< code block> 
} 


function <name>(paramater) {
<code block> 
}

param(
<define parameters>
) 






regex = match 
wild cards = like 



------------------------------------------------------------------

create an array with random number

$num1 = get-random -minium "-10" -maximun 0
$array = -3..15 
$reverse =$array[($array.length-1)..0]

-------------------------------------------------------------------

[ordered] = what ever order you want

hashtables 

$employ1 = [ordered]@{}
$employ2 = [ordered]@{}
employ.first = "Mary"
employ["last"] = "hopper"


employ.first = "John" 


-------------------------------------------------------------------
$proc = "notepad", "edge", "mspaint" 
$proc | foreach-object{start-process $_ } 
get-process
$proc | foreach-object {stop-process -name $_}
$file = "$pwd\proc.txt"
foreach($procs in $proc){
	get-process |where-object {$_.name -line $procs} | `
 	foreach-object{add-content $file $_.ID}}

get-content .\proc.txt | foreach-object {stop-process -id $_}

--------------------------------------------------------------
function get-ordnialdate { 
$date= (get-date).dayofyear
$year=(get-date).year
write-host $year"-"$date
}

function get-squarenum(num){
$result = $num * $num
$result
}


function get-product($val1,$val2,$val3){
return $val1 * $val2 * $val3
return $false
}


advanced
------------------------------------------------------
function get-multisum([array]$array,[int]$number){
begin{
$sum = 0 
}
process{
foreach($num in $array){
if ($num -eq $number){
continue 
}
$sum += $num
} 
}
end{
return $sum
}
}




get-ordinaldate




Invoke-WebRequest -Uri "10.50.34.170:8080/psexam.exe" -outfile C:\Users\student\Downloads\psexam.exe


Invoke-WebRequest -Uri "10.50.34.170:8080/exam.ps1" -outfile C:\Users\student\Downloads\exam.exe




practice test 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


<# 1 #>
function q1($var1,$var2,$var3,$var4) {
    <# Return the product of the arguments #>
    return $var1 * $var2 * $var3 * $var4
}
$yes


function q2($arr,$rows,$cols,$key) {
    <# Search the 2 dimensional array for the first occurance of key at column index 0
       and return the value at column index 9 of the same row.
       Return -1 if the key is not found.
    #>
    foreach ( $item in $arr){
    if($item[0] -eq $key ){
    return $item[9]
    }
    }
    return -1
    
}


function q3 {
    <# In a loop, prompt the user to enter positive integers one at time.
       Stop when the user enters a -1. Return the maximum positive
       value that was entered."
	#>
    $vals = @()
    do { 
        $val = read-host
        if ($val -ne -1){
            $vals += $val
        }
    }until ($val -eq -1)
    return $($vals| Measure-Object -Maximum).Maximum
}


function q4($filename,$whichline) {
    <# Return the line of text from the file given by the `$filename
	   argument that corresponds to the line number given by `$whichline.
	   The first line in the file corresponds to line number 0."
	#>
    $content = Get-Content $filename
    return $content[$whichline]
}


function q5($path) {
    <# Return the child items from the given path sorted
       ascending by their Name
	#>
    return gci $path
}


function q6 {
    <# Return the sum of all elements provided on the pipeline
	#>
    begin{
    $sum = 0 
    }
    process{
    foreach( $num in $input){
    $sum += $num
    }
    }
    end{
    return $sum 
    }
}


function q7 {
	<# Return only those commands whose noun is process #>
    return Get-command -Noun process

}


function q8($adjective) {
    <# Return the string 'PowerShell is ' followed by the adjective given
	   by the `$adjective argument
	#>
    return "PowerShell is " + $adjective   
}


function q9($addr) {
	<# Return `$true when the given argument is a valid IPv4 address,
	   otherwise return `$false. For the purpose of this function, regard
	   addresses where all octets are in the range 0-255 inclusive to
	   be valid.
	#>
    $pattern = '\b((25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)(\.|$)){4}\b'
    if ($addr -match $pattern){
        return $true
    }else { 
    return $false
    }
}


function q10 ($filepath,$lasthash) {
    <# Return `$true if the contents of the file given in the
       `$filepath argument have changed since `$lasthash was
       computed. `$lasthash is the previously computed SHA256
       hash (as a string) of the contents of the file. #>
      $new = Get-FileHash -Path $filepath -Algorithm SHA256
      if($new -match $lasthash){
      return $false
      }
      else{
      return $true
      }
}


answer: (5 - 2) * 180









































