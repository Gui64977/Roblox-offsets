```c++
constructor(uint64_t addr) {
    this->instAddr = addr;
    uint64_t container = read(addr + offsets.NameContainer, "INT64");
    if (!container || container < 0x10000) {
        this->strAddr = 0;
        return;
    }
    uint64_t str = container + offsets.Name;
    uint64_t cap = read(str + 0x18, "INT64");
    this->strAddr = cap < 16 ? str : read(str, "INT64");
}

std::string Name() {
    if (!this->IsValid() || this->strAddr == 0) return "???";
    return read(this->strAddr, "STRING");
}
```
Credits to mast3rgamers (713373865681879070)
