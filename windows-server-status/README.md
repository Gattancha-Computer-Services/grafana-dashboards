# Windows Server Status Dashboard

Overview Dashboard for Windows using Prometheus and Windows_Exporter

## Description

A comprehensive Grafana Dashboard that shows an overview of all servers, and also details stats on each server itself.

## Getting Started

### Dependencies

* Grafana - Version 11.6 or newer
* Windows Exporter v0.30.0 or newer
  
### Installing The Dashboard

* You will need to download the JSON and import it into Grafana
* When prompted use your Prometheus datasource
* You can also get the Dashboard from [Grafana.com](https://grafana.com/grafana/dashboards/16523-windows-status-prometheus/)

### Installing Windows Exporter

* Download the installer from [here](https://github.com/prometheus-community/windows_exporter)
* Copy and install this on the Windows Server you wish to install. (See below for some example install strings)

### Configuring Grafana

* Log into your Grafana server
* Open ```/etc/prometheus``` in a suitable editor, such as VIM, NANO, etc
* Depending on your setup this may or maynot already exist, but this is an example of what you need to add:
  
```
  - job_name: 'windows'
    scrape_interval: 5s
    static_configs:
      - targets: ['server1.mydomain.lab:9115','server2.mydomain.lab:9115','server2.mydomain.lab:9115']
```
* Just change the "server1.mydomain.lab" strings to your own servers and add any additional servers
* Port should match the listening port for the Windows Exporter (I use 9115)

## Help

Whilst a full description can be found on the Window Prometheus website, these are a few common ones I use for various roles:

```$installfile``` can be set as a variable in Powershell or replaced directly with the path of the MSI Install file itself
For example:
```
$installfile = "D:\Windows Exporter\windows_exporter-0.30.6-amd64.msi"
```

Hyper-V:
```
msiexec /i $InstallFile ENABLED_COLLECTORS="cache,cpu,cpu_info,cs,hyperv,logical_disk,logon,memory,net,os,process,system,tcp,time,thermalzone" LISTEN_PORT="9115" /q
```
Domain Controller: 
```
msiexec /i $InstallFile ENABLED_COLLECTORS="ad,adcs,cache,cpu,cpu_info,cs,dfsr,dhcp,dns,logical_disk,logon,memory,net,os,system,tcp,time,terminal_services" LISTEN_PORT="9115" /q
```
Generic Server:
```
msiexec /i $InstallFile ENABLED_COLLECTORS="cache,cpu,cpu_info,cs,logical_disk,logon,memory,net,os,process,system,tcp,time" LISTEN_PORT="9115" /q
```
Print Server:
```
msiexec /i $InstallFile ENABLED_COLLECTORS="cache,cpu,cpu_info,cs,logical_disk,logon,memory,net,os,printer,process,system,tcp,time" LISTEN_PORT="9115" /q
```
SCCM/ConfigMgr Server
```
msiexec /i $InstallFile ENABLED_COLLECTORS="cache,cpu,cpu_info,cs,dfsr,iis,mssql,logical_disk,logon,memory,net,os,process,tcp,time,netframework,remote_fx,service,system" LISTEN_PORT="9115" /q
```
SQL Server
```
msiexec /i $InstallFile ENABLED_COLLECTORS="cache,cpu,cpu_info,cs,mssql,logical_disk,logon,memory,net,os,process,tcp,time,netframework,remote_fx,service,system" LISTEN_PORT="9115" /q
```

## Authors

Contributors names and contact info

[@Gatt_](https://twitter.com/Gatt_)

## Version History

* 4
    * This release - Confirmed working with Grafana 11.6 and 12.0, as well as Windows Export 0.30.0

## License

This project is licensed under the GNU General Public License v3.0 License - see the LICENSE.md file for details


