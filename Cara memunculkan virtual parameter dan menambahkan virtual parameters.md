Setelah install genieACS, selanjutnya  lengkapi menu parameters seperti Tag, Action, Status, SSID, RXPower, Uptime, Secreat PPPoE, IP WAN/TR069, SN ONT, PON Type

Langkah - langkah menambahkan menu parameters:

1. Buka web genieACS, pilih menu admin > config > edit index page
   
2. Pada jendela index page masukkan perintah yang ingin ditampilkan pada halaman device, contoh:

- label: "'Tag'"
  parameter: Tags
  type: "'tags'"
- label: "'Action'"
  type: "'summon-button'"
- element: "'span.inform'"
  label: "'Status'"
  parameter: DATE_STRING(Events.Inform)
  type: "'container'"
  components:
    - type: "'parameter'"
    - chart: "'online'"
      type: "'overview-dot'"
- label: "'SSID'"
  parameter: InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.SSID
- label: "'RXPower'"
  parameter: InternetGatewayDevice.WANDevice.1.X_CMCC_GponInterfaceConfig.RXPower
- label: "'Uptime'"
  parameter: InternetGatewayDevice.WANDevice.1.WANConnectionDevice.1.WANPPPConnection.4.Uptime
- label: "'Secreat PPPoE'"
  parameter: InternetGatewayDevice.WANDevice.1.WANConnectionDevice.1.WANPPPConnection.4.Username
- label: "'IP WAN/TR069'"
  parameter: InternetGatewayDevice.WANDevice.1.WANConnectionDevice.1.WANPPPConnection.4.ExternalIPAddress
- label: "'SN ONT'"
  parameter: DeviceID.SerialNumber
- label: "'PON Type'"
  parameter: InternetGatewayDevice.WANDevice.1.WANCommonInterfaceConfig.WANAccessType
  type: "'device-link'"
  components:
    - type: "'parameter'"
- Parameter: VirtualParameter.GetPONMode

klik save untuk menyimpan editan perintahnya.

*Parameter yang dimasukkan di jendela edit index page tersebut adalah parameter yang diambil dari salah satu modem yang telah dikoneksikan ke genieACS. Ada beberapa modem yang mmeiliki parameter yang berbeda sehingga harus menambahkan parameter secara manual di virtual parameters

Pada genieACS saya yang belum muncul keterangannya yaitu menu RXPower, UPtime, Secreat PPPoE, IP WAN/TR069. Berikut langkah langkahnya

Langkah - langkah menambahkan parameter modem ke virtual parameters agar modem yang memiliki parameter berbeda dapat muncul keteranganya di halaman devices:

1. Pilih tab admin > virtual parameters > new (masukkan judul/nama yang akan ditambahkan prameter)

    a. pada genieACS saya, yang pertama klik new

        Name : rx_power
        Script : 
const now = Date.now();

let ProductClass = declare("DeviceID.ProductClass", {value: 1}).value[0];
let signal = "N/A";

switch (ProductClass) {
  case "F663NV3*":
    signal = declare("InternetGatewayDevice.WANDevice.*.X_CMCC_GponInterfaceConfig.RXPower",{value: 1}).value[0];
    break;
  default:
    let d = declare("InternetGatewayDevice.WANDevice.*.X_CMCC_GponInterfaceConfig.RXPower",{value: 1}).value[0];
    signal = Math.ceil(10 * Math.log10(d / 10000)).toString();
    break;
}

return {writable: false, value: [signal, 'xsd:string']};
klik save.

    b. yang kedua klik new
        Name : uptime
        Script : 
const now = Date.now();

let r1 = declare("InternetGatewayDevice.DeviceInfo.UpTime", {value: 1});
let r2 = declare("Device.DeviceInfo.UpTime", {value: 1});

let s = (r1 && r1.size > 0) ? r1.value[0] : ((r2 && r2.size > 0) ? r2.value[0] : 0);
if (!s) return {writable: false, value: ["N/A", 'xsd:string']};

let d = Math.floor(s / 86400), h = Math.floor((s % 86400) / 3600), m = Math.floor((s % 3600) / 60);
let hasil = (d > 0 ? d + "d " : "") + (h > 0 ? h + "h " : "") + m + "m";

return {writable: false, value: [hasil, 'xsd:string']};
klik save.

    c. yang ketiga klik new
        Name : Secreat PPPoE
        Script :
const now = Date.now();

let ProductClass = declare("DeviceID.ProductClass", {value: 1}).value[0];
let pppoe_user = "N/A";

if (/F663NV3*|F663NV9/i.test(ProductClass)) {
    let res = declare("InternetGatewayDevice.WANDevice.*.WANConnectionDevice.*.WANPPPConnection.*.Username", {value: 1});

    if (res && res.size > 0) { 
        pppoe_user = res.value[0];    }
}

return {writable: false, value: [pppoe_user, 'xsd:string']}; 
klik save.

    d. yang keempat klik new
        Name : 	IP WAN/TR069
        Script :
const now = Date.now();

let r1 = declare("InternetGatewayDevice.WANDevice.*.WANConnectionDevice.*.WANPPPConnection.*.ExternalIPAddress", {value: 1});
let r2 = declare("InternetGatewayDevice.WANDevice.*.WANConnectionDevice.*.WANPPPConnection.*.ExternalIPAddress", {value: 1});
let r3 = declare("Device.IP.Interface.*.IPv4Address.*.IPAddress", {value: 1});

let ip = (r1 && r1.size > 0 && r1.value[0] !== "0.0.0.0") ? r1.value[0] : 
         ((r2 && r2.size > 0 && r2.value[0] !== "0.0.0.0") ? r2.value[0] : 
         ((r3 && r3.size > 0) ? r3.value[0] : "N/A"));

return {writable: false, value: [ip, 'xsd:string']};
klik save.

2. Agar genieACS dapat membaca parameters modem yang berbeda, buka tab admin > config > edit index page
   
   pada nama VirtualParameters.**** nama parameter setelah tanda titik menyesuaikan nama yang dimasukkan saat membuat virtual parameters tadi, yaitu:
   
   a. yang pertama pada label : RXPower ubah parameternya menjadi VirtualParameters.rx_power
   
       - label: "'RXPower'"
   
         parameter: VirtualParameters.rx_power
   b. yang kedua pada label : Uptime ubah parameternya menjadi VirtualParameters.uptime

       - label: "'Uptime'"
   
         parameter: VirtualParameters.uptime
   c. yang ketiga pada label : Secreat PPPoE ubah parameternya menjadi VirtualParameters.secreat_PPPoE

        - label: "'Secreat PPPoE'"
   
         parameter: VirtualParameters.secreat_PPPoE
   d. yang keempat pada label : IP WAN/TR069 ubah parameternya menjadi VirtualParameters.IPWAN_TR09

        - label: "' IP WAN/TR069'"
   
         parameter: VirtualParameters.IPWAN_TR09
   
   

