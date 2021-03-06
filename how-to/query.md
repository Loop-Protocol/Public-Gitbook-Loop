# Query

### &#x20;How to send query request <a href="#how-to-send-query-request" id="how-to-send-query-request"></a>

* Command line

```
terracli query wasm contract-store <contract_address> '<JSON_formed_message>'
```

ex)

```
terracli query wasm contract-store terra18vd8fpwxzck93qlwghaj6arh4p7c5n896xzem5 '{"balance":{"address": "terra1wxe503thjmapngtnyqarxrc4jy80vf800vf0cy"}}'
```

* RESTFul API

```
<light_clinet_address>/wasm/contracts/<contract_address>/store?query_msg=<JSON_formed_message>
```

ex)

```
https://tequila-lcd.terra.dev/wasm/contracts/terra1wxe503thjmapngtnyqarxrc4jy80vf800vf0cy/store?query_msg={%22pairs%22:{}}
```

### How to oragnize query message <a href="#how-to-oragnize-query-message" id="how-to-oragnize-query-message"></a>

You may check `<contract>/src/msg.rs` of each contract.\
&#x20;Here is an example. Query messages are defined as like below:

```
#[derive(Serialize, Deserialize, Clone, Debug, PartialEq, JsonSchema)]
#[serde(rename_all = "snake_case")]
pub enum QueryMsg {
    Balance { address: HumanAddr },
    ...
}
```

This is one of the message

```
Balance { address: HumanAddr }
```

You may wrap as `{}` and change it into snake case as like below:

```
{"balance": {"address": "<HumanAddr>"}}
```

`HumanAddr` is a type, which is bech32-encoded address starting from `terra`.\
&#x20;Here is an example:

```
{"balance": {"address": "terra1wxe503thjmapngtnyqarxrc4jy80vf800vf0cy"}}
```

This rule can be applied to other messages. This overview can be helpful of contract self-study.
