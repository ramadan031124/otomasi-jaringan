# otomasi-jaringan
if config
ifconfig_psutil.py
Menampilkan informasi interface jaringan (setara dengan ifconfig -a)
tanpa memanggil perintah eksternal.
"""

import psutil

def show_interfaces():
    addrs = psutil.net_if_addrs()
    stats = psutil.net_if_stats()

    for iface_name, iface_addrs in addrs.items():
        print("=" * 60)
        print(f"Interface: {iface_name}")
        if iface_name in stats:
            st = stats[iface_name]
            print(f"  Status   : {'UP' if st.isup else 'DOWN'}")
            print(f"  MTU      : {st.mtu}")
            print(f"  Speed    : {st.speed} Mbps")
        for addr in iface_addrs:
            print(f"  {addr.family.name:10} : {addr.address}")
        print("=" * 60)

if __name__ == "__main__":
    show_interfaces()
