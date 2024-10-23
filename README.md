This is the Solana Hardware Compatibility List for running a mainnet validator.

- [Hardware Recommendations](#hardware-recommendations)
- [Compatible Hardware](#compatible-hardware)
  - [CPU](#cpu)
  - [Storage](#storage)
- [Datacenter Providers](#datacenter-providers)
- [FAQ](#faq)
- [Contributors](#contributors)
  
## Hardware Recommendations

Source: [https://github.com/anza-xyz/agave/blob/master/docs/src/operations/requirements.md](https://github.com/anza-xyz/agave/blob/master/docs/src/operations/requirements.md)

| Component | Validator Requirements | Additional RPC Node Requirements |
|-----------|------------------------|----------------------------------|
| **CPU**   | - 2.8GHz base clock speed, or faster<br />- SHA extensions instruction support<br />- AMD Gen 3 or newer<br />- Intel Ice Lake or newer<br />- Higher clock speed is preferable over more cores<br />- AVX2 instruction support (to use official release binaries, self-compile otherwise)<br />- Support for AVX512f is helpful | |
|           | 12 cores / 24 threads, or more | 16 cores / 32 threads, or more |
| **RAM**   | Error Correction Code (ECC) memory is suggested<br />Motherboard with 512GB capacity suggested | |
|           | 256GB or more | 512 GB or more for **all [account indexes](https://docs.solanalabs.com/operations/setup-an-rpc-node#account-indexing)** |
| **Disk**  | PCIe Gen3 x4 NVME SSD, or better, on each of:<br />- **Accounts**: 500GB, or larger. High TBW (Total Bytes Written)<br />- **Ledger**: 1TB or larger. High TBW suggested<br />- **Snapshots**: 250GB or larger. High TBW suggested<br />- **OS**: (Optional) 500GB, or larger. SATA OK<br /><br />The OS may be installed on the ledger disk, though testing has shown better performance with the ledger on its own disk<br /><br />Accounts and ledger *can* be stored on the same disk, however due to high IOPS, this is not recommended<br /><br />The Samsung 970 and 980 Pro series SSDs are popular with the validator community | Consider a larger ledger disk if longer transaction history is required<br /><br />Accounts and ledger **should not** be stored on the same disk |
| **GPUs**  | Not necessary at this time<br />Operators in the validator community do not use GPUs currently | |

## Compatible Hardware

### CPU

AMD is the CPU of choice when it comes to running Solana validators. Intel Xeon Gold/Platinum (6[45]xx) are the only ones known to be able to keep up with the chain.
This list is not exhaustive, just a selection of CPUs different folks on the discord have run or are currently running. 24 cores is the sweet spot, as of 10/2024. 
12/16cores will most likely struggle and more than 32 cores will have a slower base clock speed due to TDP issues. 32 cores would possibly be more future proof.

| Recommended  | Manufacturer | Model                              | Base Clock | Max Boost Clock | Cores | Threads | Default TDP |
|--------------|--------------|------------------------------------|------------|-----------------|-------|---------|-------------|
| Yes          | **AMD**      | Ryzen™ Threadripper™ PRO 7965WX    | 4.2 GHz    | Up to 5.3 GHz   | 24    | 48      | 350W        |
| Yes          | **AMD**      | Ryzen™ Threadripper™ PRO 7975WX    | 4.0 GHz    | Up to 5.3 GHz   | 32    | 64      | 350W        |
| Yes          | **AMD**      | Ryzen™ Threadripper™ PRO 7985WX    | 3.2 GHz    | Up to 5.1 GHz   | 64    | 128     | 350W        |
| Yes          | **AMD**      | AMD EPYC™ 9274F                    | 4.05 GHz   | Up to 4.3 GHz   | 24    | 48      | 320W        |
| Yes          | **AMD**      | AMD EPYC™ 9275F                    | 4.1 GHz    | Up to 4.8 GHz   | 24    | 48      | 320W        |
| Yes          | **AMD**      | Ryzen™ Threadripper™ 7960X         | 4.2 GHz    | Up to 5.3 GHz   | 24    | 48      | 350W        |
| Yes          | **AMD**      | AMD EPYC™ 74F3                     | 3.2 GHz    | Up to 4.0 GHz   | 24    | 48      | 240W        |
| Yes          | **AMD**      | AMD EPYC™ 9254                     | 2.9 GHz    | Up to 4.15 GHz  | 24    | 48      | 200W        |
| Yes          | **AMD**      | AMD EPYC™ 9354P                    | 3.25 GHz   | Up to 3.8 GHz   | 32    | 64      | 280W        |
| Barely       | **AMD**      | AMD EPYC™ 7443P                    | 2.85 GHz   | Up to 4.0 GHz   | 24    | 48      | 200W        |

These recommendations also work for RPC nodes, but RPC nodes require more cores and RAM to perform better under load

Source:
- [AMD Server Processors](https://www.amd.com/en/products/specifications/server-processor.html)
- [AMD Workstation Processors](https://www.amd.com/en/products/specifications/processors.html)

### Storage

**Enterprise**

| Manufacturer | Model         | Sequential Read | Sequential Write | Random Read (IOPS) | Random Write (IOPS) |
|--------------|---------------|-----------------|------------------|--------------------|---------------------|
| **Kioxia**   | CM7-R (3.8tb) | 14,000 MB/s     | 7,000 MB/s       | 2,700,000 IOPS     | 310,000 IOPS        |
| **Samsung**  | PM9A1         | 7,000 MB/s      | 5,200 MB/s       | 1,000,000 IOPS     | 850,000 IOPS        |
| **Samsung**  | PM9A3         | 6,800 MB/s      | 2,700 MB/s       | 850,000 IOPS       | 130,000 IOPS        |
| **Micron**   | 7450          | 6,800 MB/s      | 5,300 MB/s       | 1,500,000 IOPS     | 550,000 IOPS        |

**Consumer**

| Manufacturer | Model         | Sequential Read | Sequential Write | Random Read (IOPS) | Random Write (IOPS) |
|--------------|---------------|-----------------|------------------|--------------------|---------------------|
| **Crucial**  | T705          | 14,500MB/s      | 12,700MB/s       | 1,550,000 IOPS     | 1,800,000 IOPS      |
| **WD**       | SN850X        | 7,300 MB/s      | 6,600 MB/s       | 1,200,000 IOPS     | 1,000,000 IOPS      |
| **Samsung**  | 990 Pro       | 7,450 MB/s      | 6,900 MB/s       | 1,400,000 IOPS     | 1,550,000 IOPS      |
| **Samsung**  | 980 Pro       | 7,000 MB/s      | 5,100 MB/s       | 1,000,000 IOPS     | 1,000,000 IOPS      |

## Datacenter Providers

| Provider     | Link                                                                 | Notes                                  |
|--------------|----------------------------------------------------------------------|----------------------------------------|
| **Latitude** | [Latitude](https://latitude.sh)                                      | Widely used by Solana validators, yearly contracts, API access |
| **Edgevana** | [Edgevana](https://srv.edgevana.com/solana-validator-servers)        | Tailored specifically for Solana validators, accepts crypto |
| **Teraswitch**| [Teraswitch](https://teraswitch.com/bare-metal/)                    | Widely used by Solana validators |
| **Vultr**    | [Vultr](https://www.vultr.com/pricing/#bare-metal)                  | Affordable bare-metal options, worldwide datacenter locations, per hour pricing, accepts crypto |
| **Cherry**   | [Cherry](https://www.cherryservers.com/bare-metal-dedicated-servers) | API access, possibly oversold bandwidth, good availability |
| **OVH**      | [OVH](https://ovhcloud.com/)                                         | Large provider, but beware of over-aggressive DDoS mitigation, which may impact Solana performance |

More here: [Marinade ISP list](https://app.marinade.finance/network/isps/?countries=&direction=descending&sorting=stake)
---

### Notes

- **CPU Selection:** Prioritize CPUs with higher base clock speeds to meet Solana validator performance requirements. Ensure the selected CPU supports at least AVX2 instructions, with AVX-512 providing additional performance benefits. The AMD Ryzen™ Threadripper™ PRO and AMD EPYC™ series listed above are optimized for high-performance and multi-threaded tasks essential for validator operations.

- **Storage Selection:** Choose NVMe SSDs that offer high IOPS to handle the intensive read/write operations necessary for validator nodes. Samsung's Pro series and WD's SN850X are highly recommended for their reliability and performance within the validator community.

- **Memory Considerations:** While not part of the table, remember that **RAM** requirements are crucial. Ensure you have ECC memory and sufficient capacity as per the [Hardware Recommendations](#hardware-recommendations) section. RAM **speed** and DDR4 vs DDR5 are not known to make any significant differences 

Feel free to reach out if you need further assistance or more detailed specifications!

## FAQ

Q: My validator doesn't catch up or catches up slowly or does not keep up with the tip

A: If you've followed the [setup instructions](https://docs.solanalabs.com/operations/setup-a-validator) correctly, make sure to:
  (via [ax on discord](https://discord.com/channels/428295358100013066/1187805174803210341/1288757805062553600))

  i would like to suggest using the acronym "core" when beginners are asking for help, because its always the same question with same answers. it helps to break down the steps and make the guidance easier to follow:
- c: check cpu performance (focus on single-thread speeds)
- o: optimize nvme by separating ledger and accounts
- r: remove unnecessary cli arguments
- e: enable performance mode 

this way we can give quick, clear advice thats easy to remember. we could pin and refer to it. what do you think?

### setup performance mode

```sudo apt install cpufrequtils```

```sudo bash -c 'echo performance > /sys/devices/system/cpu/cpu*/cpufreq/scaling_governor'```

--

## Contributors

- [ferric](https://x.com/ferric) / [StakeWare](https://stakeware.xyz)

### Inspired by
- [Zan](https://x.com/shinobisystems)
- [/dev/null](https://x.com/pumpkinspool)
- ax / [1000x.sh](https://1000x.sh)
- meyerbro
- [7layer](https://x.com/7LayerMagik) / [Overclock](https://overclock.one)
- Everyone else on #validator-hw-tuning
