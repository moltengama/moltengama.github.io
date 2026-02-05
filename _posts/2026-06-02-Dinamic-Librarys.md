---
title: "Dinamic Librarys"
date: 2026-02-03 00:00:00 +0800
categories: [maldev, c++,c]
tags: [maldev, c++,c,programming]
image:
  path: /assets/img/banners/b1d89d5f598fac58eb96512b3527ec01.jpg
---
  
  

## METODOS DE CARGA DE DLL:


#### Ruta Especifica
``` c++
 HMODULE hModule = LoadLibraryA("C:\\Users\\gama\\source\\repos\\Dll1\\x64\\Release\\DLL1.dll");

```
#### En memoria:
```c++
 HMODULE kernel321 = GetModuleHandleA("kernel32.dll");
```

##### Carga de funciones:
``` c++
typedef BOOL (WINAPI* {nombre del puntero para la funcion})([Lista de parametros que necesita la funcion]);
PVOID DireccionFuncion = GetProcAddress(hmodule, "<FuncionEspecifica.>"); // Obtener direccion de memoria de la funcion

NombreDePuntero funcionref =(NombreDePuntero)DireccionFuncion;
funcionref(Parametros);
```



### Ejemplos:

Con una libreria personalizada `DLL1.dll` accederemos a la funcion especifica `lovelive` (Al no recibir parametreos el tipo de puntero sera vacio)
``` c++

int maine() {
    // Load the DLL
    HMODULE hModule = LoadLibraryA("C:\\Users\\gama\\source\\repos\\Dll1\\x64\\Release\\DLL1.dll"); 
    printf("Direccion del dll: %p \n", hModule);
    PVOID plovelive = GetProcAddress(hModule, "lovelive");
    printf("Direccion funcion de hellowordl: %p \n", plovelive);
    DWORD error = GetLastError();
    cout << error;

    loveliveFunctionPointer lovelive =(loveliveFunctionPointer)plovelive;
    lovelive();
    getchar();
    return 0;
}

``` 

Usando a libreria `kernel32.dll` aprovecharemos cargas sus funciones de forma directa con la api de windows para obtener informacion del sistema:

```  c++

typedef void (WINAPI* fpsysteminfo)(LPSYSTEM_INFO);

int mainE3() {
    HMODULE kernel321 = GetModuleHandleA("kernel32.dll");
    PVOID psysinfo = GetProcAddress(kernel321, "GetSystemInfo");
    printf("SystemInfoFunc: %p ", psysinfo);

    fpsysteminfo sysinfo_func = (fpsysteminfo)psysinfo;

    SYSTEM_INFO si;
    ZeroMemory(&si, sizeof(si));
    sysinfo_func(&si);
    printf("=== SYSTEM INFO ===\n");
    printf("ProcessorArchitecture : %u\n", si.wProcessorArchitecture);
    printf("PageSize              : %lu\n", si.dwPageSize);
    printf("MinAppAddress         : %p\n", si.lpMinimumApplicationAddress);
    printf("MaxAppAddress         : %p\n", si.lpMaximumApplicationAddress);
    printf("ActiveProcessorMask   : %p\n", (void*)si.dwActiveProcessorMask);
    printf("NumberOfProcessors    : %lu\n", si.dwNumberOfProcessors);
    printf("ProcessorType         : %lu\n", si.dwProcessorType);
    printf("AllocationGranularity : %lu\n", si.dwAllocationGranularity);
    printf("ProcessorLevel        : %u\n", si.wProcessorLevel);
    printf("ProcessorRevision     : %u\n", si.wProcessorRevision);
    return 0;
}

}
``` 


Abrir una terminal usando las funcioens de `kernel32.dll` con `CreateProcessA`
```  c++
typedef BOOL (WINAPI* pcmde)(LPCSTR, LPSTR, LPSECURITY_ATTRIBUTES, LPSECURITY_ATTRIBUTES, BOOL, DWORD, LPVOID, LPCSTR, LPSTARTUPINFOA, LPPROCESS_INFORMATION);

int main() {

    HMODULE kernel321 = GetModuleHandleA("kernel32.dll");
    PVOID pcreateProcess = GetProcAddress(kernel321, "CreateProcessA");
    printf("CreateProcessDIR: %p ", pcreateProcess);
    pcmde crearproceso = (pcmde)pcreateProcess;
    LPCSTR bina = "C:\Windows\System32\cmd.exe";

    STARTUPINFOA si{};
    si.cb = sizeof(si);

    PROCESS_INFORMATION pi{};
    char cmdLine[] = "cmd.exe /k powershell.exe  -c whoami";


    BOOL ok = crearproceso(
        "C:\\Windows\\System32\\cmd.exe", // lpApplicationName
        cmdLine,                              // lpCommandLine (o una línea de comandos)
        NULL,                              // lpProcessAttributes
        NULL,                              // lpThreadAttributes
        FALSE,                             // bInheritHandles
        0,                                 // dwCreationFlags
        NULL,                              // lpEnvironment
        NULL,                              // lpCurrentDirectory
        &si,                               // lpStartupInfo
        &pi                                // lpProcessInformation
    );
    
}


```

> Todas las funciones apuntadas para usarlas debemos cargar y pasar todos sus parametros que solicita no obviar ninguno

