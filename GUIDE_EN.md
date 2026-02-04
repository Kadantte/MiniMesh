# User Guide: Installing and Running the MiniMesh Module

中文说明书在这里>>> [GUIDE_CN.md](https://github.com/linser233/MiniMesh/blob/main/GUIDE_CN.md)  

## Hardware Installation Steps

1. **Attach the antenna**  
   - Firmly screw the antenna onto the corresponding RF SMA connector.  
   - ⚠️⚠️⚠️ **Warning: Never power on the device without the antenna attached, otherwise permanent damage to MiniMesh will occur.**  

2. **Plugged into the device’s USB connector**

---

## Software Configuration Steps

6. **Power on and install meshtasticd**  
   - Boot into Linux and install meshtasticd following the official documentation:  
     [Meshtastic Linux Installation Guide](https://meshtastic.org/docs/software/linux/installation)  

7. **Obtain and place the configuration file**  
   - Visit the repositories [meshtastic/firmware official GitHub](https://github.com/meshtastic/firmware/tree/develop/bin/config.d) or [MiniMesh GitHub](https://github.com/linser233/MiniMesh).  
   - Based on the PCB or packaging label of your module, download either `lora-usb-minimesh-1262.yaml` or `lora-usb-minimesh-1268.yaml`.  
   - Place the file into the configuration directory:  
     ```bash
     sudo cp lora-usb-minimesh-126*.yaml /etc/meshtasticd/config.d/
     ```  
   - 💡 **Tip:** This step is usually handled automatically. Manual action is only required if you need to adjust transmit power or if `auto` detection does not work properly.  

8. **Start or restart the meshtasticd service**  
   - Manage the service with systemd:  
     ```bash
     sudo systemctl enable meshtasticd
     sudo systemctl restart meshtasticd
     ```  

9. **Begin using**  
   - Verify node information:  
     ```bash
     meshtastic --info
     ```  
   - If you can see `firmware_version`, `my_node_id`, and other details, the configuration is successful.  
   - 🎉🎉🎉 Enjoy your Meshtastic network!  

---

## Tips & Notes

- **Unexpected reboot or insufficient power**  
  If unexpected reboots or power shortages occur, edit the `lora-usb-minimesh-126*.yaml` file and set:  
  ```yaml
  SX126X_MAX_POWER: 22
  ```  
  ⚠️ This option is subject to **local regulations** and **hardware limitations**. Please comply accordingly.  

- **Antenna matching**  
  Use an antenna that matches the module’s frequency band (e.g., CN470, EU868, US915) to avoid damage or degraded performance.  