# Comandos de procesos Windows

## Totales genérico
````
Get-Process
# Handlecount, ProcessName, NonpagedSystemMemorySize, PagedMemorySize, VirtualMemorySize, WorkingSet, TotalProcessorTime
# Handles: The number of handles that the process has opened.
# NPM(K): The amount of non-paged memory that the process is using, in kilobytes.
# PM(K): The amount of pageable memory that the process is using, in kilobytes.
# WS(K): The size of the working set of the process, in kilobytes. The working set consists of the pages of memory that were recently referenced by the process.
# VM(M): The amount of virtual memory that the process is using, in megabytes. Virtual memory includes storage in the paging files on disk.
# CPU(s): The amount of processor time that the process has used on all processors, in seconds.
# ID: The process ID (PID) of the process.
# ProcessName: The name of the process. 
Get-WmiObject -Class Win32_process
Get-ciminstance Win32_process
Get-Process
# Handlecount, ProcessName, NonpagedSystemMemorySize, PagedMemorySize, VirtualMemorySize, WorkingSet, TotalProcessorTime
# Handles: The number of handles that the process has opened.
# NPM(K): The amount of non-paged memory that the process is using, in kilobytes.
# PM(K): The amount of pageable memory that the process is using, in kilobytes.
# WS(K): The size of the working set of the process, in kilobytes. The working set consists of the pages of memory that were recently referenced by the process.
# VM(M): The amount of virtual memory that the process is using, in megabytes. Virtual memory includes storage in the paging files on disk.
# CPU(s): The amount of processor time that the process has used on all processors, in seconds.
# ID: The process ID (PID) of the process.
# ProcessName: The name of the process. 
Get-WmiObject -Class Win32_process
Get-ciminstance Win32_process
````
## Mediciones
````
Get-Process | measure -Property CPU -Sum -Average -Max -Min
````
## Obtener información completa
````
Get-Process | select -Property *
Get-WmiObject -Class Win32_process | select -Property *
Get-Ciminstance Win32_process | select -Property *
````

## Filtrado
````
#forma directa
Get-Process -Id 4
Get-Process -Name AdobeUpdateService
Get-WmiObject -Class Win32_process -Filter ("name='AdobeUpdateService.exe'")

#evaluando sus propiedades
Get-Process | Where-Object {$_.BasePriority -lt 10}
Get-WmiObject -Class Win32_process | Where-Object {$_.Priority -gt 8}
````

## Modificar prioridades
````
Get-Process -Name notepad | select Name,BasePriority, PriorityClass
#las posibles prioridades son "Idle, BelowNormal, Normal, AboveNormal, High, RealTime"
(Get-Process -Name notepad).PriorityClass = "Idle"
$procesos = Get-Process | Where-Object {$_.BasePriority -lt 5}
foreach($i in $procesos){
    $i.PriorityClass = "Normal"
}
Get-Process -Name notepad | select Name,BasePriority, PriorityClass
#las posibles prioridades son Idle, BelowNormal, Normal, AboveNormal, High, RealTime"
(Get-Process -Name notepad).PriorityClass = "Idle"
$procesos = Get-Process | Where-Object {$_.BasePriority -lt 5}
foreach($i in $procesos){
    $i.PriorityClass = "Normal"
}
````

# Eventos
````
# escuchar acciones de procesos arrancados
Register-WmiEvent -Class Win32_ProcessStartTrace -SourceIdentifier abiertos -Action $accion1
# escuchar acciones de procesos parados
Register-WmiEvent -Class Win32_ProcessStopTrace -SourceIdentifier cerrados -Action $accion2
````
