
## Schema

### Structure

```mermaid
graph TD
    A[car_model]
    B[feature]
    C[part]
    D[supplier]

    A -->|with_feature| B
    A -->|is_composed_of| C
    C -->|is_supplied_by| D

    style A fill:#f9d,stroke:#333,stroke-width:2px;
    style B fill:#fcc,stroke:#333,stroke-width:2px;
    style C fill:#cfc,stroke:#333,stroke-width:2px;
    style D fill:#ccf,stroke:#333,stroke-width:2px;
```

### Properties

```mermaid
classDiagram
    class car_model {
        string name
        string number
        int year
        string type
        string engine_type
        string size
        int seats
    }
    class feature {
        string name
        string number
        string type
        string state
    }
    class part {
        string name
        string number
        double price
        timestamp date
    }
    class supplier {
        string name
        string address
        string contact
        string phone_number
    }

    car_model --> feature : with_feature
    car_model --> part : is_composed_of
    part --> supplier : is_supplied_by
```

## DDL

```sql
CREATE SPACE IF NOT EXISTS auto_manufacturing_supply_chain (vid_type=FIXED_STRING(64), partition_num=1, replica_factor=1);

CREATE TAG IF NOT EXISTS car_model(name string, number string, year int, type string, engine_type string, size string, seats int);
CREATE TAG IF NOT EXISTS feature(name string, number string, type string, state string);
CREATE TAG IF NOT EXISTS part(name string, number string, price double, date timestamp);
CREATE TAG IF NOT EXISTS supplier(name string, address string, contact string, phone_number string);

CREATE EDGE IF NOT EXISTS with_feature(version string);
CREATE EDGE IF NOT EXISTS is_composed_of(version string);
CREATE EDGE IF NOT EXISTS is_supplied_by(version string);
```

## Credits

The idea of this dataset comes from Julia XIAO, the Customer Success Engineer of NebulaGraph.

Due to I don't have bandwidth to prepare the datagen this time, I instead tried to ask ChatGPT-4 to help generate a small sample data first. See [here](https://chat.openai.com/share/10413cc3-8d4a-4795-88a2-3d231e4cfd9c) for the chat log.
