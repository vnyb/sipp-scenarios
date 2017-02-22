# SIPp scenarios

This is a collection of SIPp scenarios for testing purposes.

SIPp - download and documentation: http://sipp.sourceforge.net

Thanks: https://github.com/saghul/sipp-scenarios

# Scenarios

<!-- LIST-BEGIN -->
| Name | Description |
|------|-------------|
| `sipp_uac_audio_video.xml` | UAC audio-video |
| `sipp_uac_basic.xml` | UAC basic |
| `sipp_uac_pcap_g711a.xml` | UAC audio PCM-A 8000 (G.711) |
| `sipp_uas_basic.xml` | UAS basic |
| `sipp_uas_delayed_answer.xml` | UAS delayed answer |
| `sipp_uas_pcap_g711a.xml` | UAS audio PCM-A 8000 (G.711) |
<!-- LIST-END -->

# Use cases

## Success call (without RTP)

Server side:
```bash
sipp -sf sipp_uas_basic.xml -i <server address> -p 5060
```

Client side:
```bash
sipp -sf sipp_uac_basic.xml -m 1 <server address>:5060
```

