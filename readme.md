[![GitHub](https://img.shields.io/github/license/jkulvich/intelpower)](https://github.com/jkulvich/intelpower/blob/master/LICENSE)
[![GitHub go.mod Go version](https://img.shields.io/github/go-mod/go-version/jkulvich/intelpower)](https://blog.golang.org/go1.13)
[![Go Report Card](https://goreportcard.com/badge/jkulvich/intelpower)](http://goreportcard.com/report/jkulvich/intelpower)
[![GoDoc](https://godoc.org/github.com/jkulvich/intelpower?status.svg)](https://godoc.org/github.com/jkulvich/intelpower)
[![GitHub release (latest by date)](https://img.shields.io/github/v/release/jkulvich/intelpower)](https://github.com/jkulvich/intelpower/releases)
[![GitHub last commit](https://img.shields.io/github/last-commit/jkulvich/intelpower)](https://github.com/jkulvich/intelpower/commits/master)
[![GitHub issues](https://img.shields.io/github/issues/jkulvich/intelpower)](https://github.com/jkulvich/intelpower/issues)
[![CPU support](https://img.shields.io/badge/CPU%20min.%20family%20support-Intel%20Sandy%20Bridge-blue)](https://en.m.wikipedia.org/wiki/Sandy_Bridge)

[![Repo moved](https://img.shields.io/badge/MOVED-gopowersupply%2Fintelcpu-red)](https://github.com/gopowersupply/intelcpu)

# What is it?

Intel CPU control package.  
Documentation can be [found here](https://godoc.org/github.com/jkulvich/intelpower).

# Requirements

- `intel_pstate` CPU Performance Scaling Driver

# Example

```go
pwr := intelpower.New()

if err := pwr.CheckDriver(); err != nil {
	panic(err)
}

stat, _ := pwr.GetStatus()
switch stat {
case PStateStatusActive:
	fmt.Println("All is ok")
case PStateStatusPassive:
	fmt.Println("Some troubles, some actions maybe ignored")
case PStateStatusOff:
	fmt.Println("Driver is off, actions won't take effects")
}

// CPU name
cpuName, _ := pwr.GetCPUName()

// temperature from main thermal sensor
temp, _ := pwr.GetTemp()

// TurboBoost checking and enabling
if turbo, _ := pwr.IsTurbo(); !turbo {
	pwr.SetTurbo(true)
}

// Always maximum frequency
_ := pwr.GetMinPerf(1)

// Working with CPUs
cpus, _ := pwr.GetCPUs()

// CPU frequency
freq, _ := cpus[0].GetFreq()
baseFreq, _ := cpus[0].GetBaseFreq()
maxFreq, _ := cpus[0].GetMaxFreq()
minFreq, _ := cpus[0].GetMinFreq()

// CPU disabling
cpus[3].SetOnline(false)

// CPU governor mode
cpus[3].SetGovernor(CPUGovernorPerformance)

// CPU preference mode
cpus[3].SetPreference(CPUPreferencePerformance)

```
