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

## Success call (with RTP)

Server side:
```bash
sipp -sf sipp_uas_pcap_g711a.xml -i <server address> -mi <server address> -mp 6000
```

Client side:
```bash
sipp -sf sipp_uac_pcap_g711a.xml -m 1 -i <client address> -mi <client address> -mp 6000 <server address>:5060
```

## Busy callee

Server side:
```bash
sipp -sf sipp_uas_486_busy.xml -i <server address> -p 5060
```

Client side:
```bash
sipp -sf sipp_uac_basic.xml -m 1 <server address>:5060
```

## Callee does not answer, caller cancels the request

Server side:
```bash
sipp -sf sipp_uas_no_answer.xml -i <server address> -p 5060
```

Client side:
```bash
sipp -sf sipp_uac_cancel.xml -m 1 <server address>:5060
```

## Callee rejects the call

Server side:
```bash
sipp -sf sipp_uas_403_forbidden -i <server address> -p 5060
```

Client side:
```bash
sipp -sf sipp_uac_basic.xml -m 1 <server address>:5060
```

## Multi-party call (with RTP)

It is possible simulate a multi-party call using `sipp_uac_pcap_g711a.xml` and `sipp_uas_pcap_g711a.xml` scenario files. In this example, Alice and Bob both call Charlie. In a real use case, Charlie is supposed to mix his own stream with the Alice one to send it to Bob in a single RTP audio session. In the same way, Charlie is supposed to mix his own stream with the Bob on to send it to Alice.

Charlie side:
```bash
sipp -sf sipp_uas_pcap_g711a.xml -i <Charlie's address> -mi <Charlie's address> -mp 6000
```

Bob side:
```bash
sipp -sf sipp_uac_pcap_g711a.xml -m 1 -i <Bob's address> -mi <Bob's address> -mp 6000 <Charlie's address>:5060
```

Alice side:
```bash
sipp -sf sipp_uac_pcap_g711a.xml -m 1 -i <Alice's address> -mi <Alice's address> -mp 6000 <Charlie's address>:5060
```

