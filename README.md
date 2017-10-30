# nodered code running a routine to record data at Amazon RC2 MySql
[
    {
        "id": "6d6af18f.ed5e1",
        "type": "catch",
        "z": "50f61338.29072c",
        "name": "",
        "scope": null,
        "x": 412.77771759033203,
        "y": 134.49996376037598,
        "wires": [
            [
                "3808821b.04723e",
                "d2415f3f.c1009"
            ]
        ]
    },
    {
        "id": "1670be23.2e9432",
        "type": "modbus-queue-info",
        "z": "50f61338.29072c",
        "name": "Fila Leitura GMG1 Remoto",
        "unitid": "1",
        "lowLowLevel": 25,
        "lowLevel": 75,
        "highLevel": 150,
        "highHighLevel": 300,
        "server": "986a090a.461d98",
        "errorOnHighLevel": false,
        "x": 988.9999732971191,
        "y": 111.61108875274657,
        "wires": [
            [
                "7a36282e.d3ddb8"
            ]
        ]
    },
    {
        "id": "3808821b.04723e",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Reseta leitura se atingir nivel high high",
        "func": "if(\"high high level reached\" === msg.state && \n    msg.unitid === 1 &&\n    msg.error.source.name === \"Read Queue\") {\n    msg.resetQueue = true;\n    return msg;\n}\n",
        "outputs": 1,
        "noerr": 0,
        "x": 678.1110420227051,
        "y": 112.72218251228331,
        "wires": [
            [
                "1670be23.2e9432"
            ]
        ]
    },
    {
        "id": "7a36282e.d3ddb8",
        "type": "debug",
        "z": "50f61338.29072c",
        "name": "",
        "active": false,
        "console": "false",
        "complete": "false",
        "x": 1229.666561126709,
        "y": 119.83332443237303,
        "wires": []
    },
    {
        "id": "f1d7e869.d34ec8",
        "type": "inject",
        "z": "50f61338.29072c",
        "name": "Selecionar 5 a 10s por GMG",
        "topic": "",
        "payload": "",
        "payloadType": "date",
        "repeat": "10",
        "crontab": "",
        "once": false,
        "x": 159.2857208251953,
        "y": 306.56355381011963,
        "wires": [
            [
                "3ed12873.e59758",
                "1a987d11.5b8463",
                "b3f15fdf.6a854",
                "d3d38163.a70bd",
                "851fc10b.59006",
                "733e8745.b77128"
            ]
        ]
    },
    {
        "id": "3ed12873.e59758",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Lê 1 a 95 (IR)",
        "func": "msg.payload = { input: msg.payload, 'fc': 4, 'unitid': 1, 'address': 0 , 'quantity': 94 }\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 428.9444160461426,
        "y": 226.27777123451233,
        "wires": [
            [
                "122adf6a.49b9c1"
            ]
        ]
    },
    {
        "id": "122adf6a.49b9c1",
        "type": "modbus-flex-getter",
        "z": "50f61338.29072c",
        "name": "Envia Fila de Leitura GMG1",
        "showStatusActivities": false,
        "showErrors": false,
        "server": "986a090a.461d98",
        "x": 650.0000495910645,
        "y": 223.27778911590576,
        "wires": [
            [
                "f9b6e5ed.7f0108"
            ],
            []
        ]
    },
    {
        "id": "1a987d11.5b8463",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Lê 354-359 (IR)",
        "func": "msg.payload = { input: msg.payload, 'fc': 4, 'unitid': 1, 'address': 353 , 'quantity': 7 }\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 435.44443130493164,
        "y": 266.2777681350708,
        "wires": [
            [
                "dcdf0355.85a7c"
            ]
        ]
    },
    {
        "id": "d3d38163.a70bd",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Lê 1-25 (HR)",
        "func": "msg.payload = { input: msg.payload, 'fc': 3, 'unitid': 1, 'address': 0 , 'quantity': 26 }\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 427.666690826416,
        "y": 362.61114025115967,
        "wires": [
            [
                "63cf5ac3.63ec24"
            ]
        ]
    },
    {
        "id": "dcdf0355.85a7c",
        "type": "modbus-flex-getter",
        "z": "50f61338.29072c",
        "name": "Envia Fila de Leitura GMG1",
        "showStatusActivities": false,
        "showErrors": false,
        "server": "986a090a.461d98",
        "x": 652.4444313049316,
        "y": 265.2777681350708,
        "wires": [
            [
                "9a50ebc6.8fb938"
            ],
            []
        ]
    },
    {
        "id": "63cf5ac3.63ec24",
        "type": "modbus-flex-getter",
        "z": "50f61338.29072c",
        "name": "Envia Fila de Leitura GMG1",
        "showStatusActivities": false,
        "showErrors": false,
        "server": "986a090a.461d98",
        "x": 655.666690826416,
        "y": 358.61114025115967,
        "wires": [
            [
                "e95609c4.49c0e8"
            ],
            []
        ]
    },
    {
        "id": "2a03d611.26c39a",
        "type": "mysql",
        "z": "50f61338.29072c",
        "mydb": "20d837e1.532ea8",
        "name": "",
        "x": 1500.714656829834,
        "y": 392.92881774902344,
        "wires": [
            []
        ]
    },
    {
        "id": "b3f15fdf.6a854",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Lê 132 (IR)",
        "func": "msg.payload = { input: msg.payload, 'fc': 4, 'unitid': 1, 'address': 131 , 'quantity': 1 }\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 419.7777442932129,
        "y": 312.61108112335205,
        "wires": [
            [
                "3ba82fb3.712d7"
            ]
        ]
    },
    {
        "id": "3ba82fb3.712d7",
        "type": "modbus-flex-getter",
        "z": "50f61338.29072c",
        "name": "Envia Fila de Leitura GMG1",
        "showStatusActivities": false,
        "showErrors": false,
        "server": "986a090a.461d98",
        "x": 646.7777442932129,
        "y": 311.61108112335205,
        "wires": [
            [
                "8568d612.5fc9c8"
            ],
            []
        ]
    },
    {
        "id": "72e33e29.eafac",
        "type": "modbus-server",
        "z": "50f61338.29072c",
        "name": "Local",
        "logEnabled": false,
        "serverPort": 10502,
        "responseDelay": "10",
        "delayUnit": "ms",
        "coilsBufferSize": 1024,
        "holdingBufferSize": 1024,
        "inputBufferSize": 1024,
        "x": 413.00009536743164,
        "y": 64.66666412353516,
        "wires": [
            [
                "a80e98e1.25ce78"
            ],
            [
                "a80e98e1.25ce78"
            ],
            [
                "a80e98e1.25ce78"
            ]
        ]
    },
    {
        "id": "a80e98e1.25ce78",
        "type": "debug",
        "z": "50f61338.29072c",
        "name": "",
        "active": false,
        "console": "false",
        "complete": "true",
        "x": 611.1667308807373,
        "y": 64.83335113525389,
        "wires": []
    },
    {
        "id": "d2415f3f.c1009",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Reseta escrita se atingir nivel high high",
        "func": "if(\"high high level reached\" === msg.state && \n    msg.unitid === 1 &&\n    msg.error.source.name === \"Write Queue\") {\n    msg.resetQueue = true;\n    return msg;\n}\n",
        "outputs": 1,
        "noerr": 0,
        "x": 691.6665916442871,
        "y": 156.49999618530273,
        "wires": [
            [
                "225b097.36dcbf6"
            ]
        ]
    },
    {
        "id": "225b097.36dcbf6",
        "type": "modbus-queue-info",
        "z": "50f61338.29072c",
        "name": "Fila Escrita GMG1 Local",
        "unitid": "1",
        "lowLowLevel": "5",
        "lowLevel": "10",
        "highLevel": "15",
        "highHighLevel": "30",
        "server": "a8d40646.cef038",
        "errorOnHighLevel": true,
        "x": 979.666820526123,
        "y": 157.83332920074463,
        "wires": [
            [
                "7a36282e.d3ddb8"
            ]
        ]
    },
    {
        "id": "f893240.bcc15e",
        "type": "modbus-write",
        "z": "50f61338.29072c",
        "name": "Salva GMG1 Local",
        "showStatusActivities": true,
        "showErrors": true,
        "unitid": "1",
        "dataType": "MHoldingRegisters",
        "adr": "0",
        "quantity": "38",
        "server": "a8d40646.cef038",
        "x": 1121.8888778686523,
        "y": 216.94452953338623,
        "wires": [
            [],
            []
        ]
    },
    {
        "id": "851fc10b.59006",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Lê GMG1 local",
        "func": "msg.payload = { input: msg.payload, 'fc': 3, 'unitid': 1, 'address': 0 , 'quantity': 55 }\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 425.4762840270996,
        "y": 407.6430730819702,
        "wires": [
            [
                "923eec35.c3801"
            ]
        ]
    },
    {
        "id": "923eec35.c3801",
        "type": "modbus-flex-getter",
        "z": "50f61338.29072c",
        "name": "Envia Fila de Leitura GMG1 Local",
        "showStatusActivities": false,
        "showErrors": false,
        "server": "a8d40646.cef038",
        "x": 668.4602928161621,
        "y": 412.30969524383545,
        "wires": [
            [
                "7f407240.c1491c"
            ],
            []
        ]
    },
    {
        "id": "81c8a512.5160a8",
        "type": "modbus-write",
        "z": "50f61338.29072c",
        "name": "Salva GMG1 Local",
        "showStatusActivities": true,
        "showErrors": true,
        "unitid": "1",
        "dataType": "MHoldingRegisters",
        "adr": "38",
        "quantity": "4",
        "server": "a8d40646.cef038",
        "x": 1117.8018836975098,
        "y": 262.0081305503845,
        "wires": [
            [],
            []
        ]
    },
    {
        "id": "f9b6e5ed.7f0108",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Separa Dados",
        "func": "var todos = {payload: [\nmsg.payload[0], //1   busbar_voltage_12 LSB\nmsg.payload[1], //2   busbar_voltage_12 MSB\nmsg.payload[2], //3   busbar_voltage_23 LSB\nmsg.payload[3], //4   busbar_voltage_23 MSB\nmsg.payload[4], //5   busbar_voltage_31 LSB\nmsg.payload[5], //6   busbar_voltage_31 MSB\nmsg.payload[6], //7   generator_voltage_12 LSB\nmsg.payload[7], //8   generator_voltage_12 MSB\nmsg.payload[8], //9   generator_voltage_23 LSB\nmsg.payload[9], //10  generator_voltage_23 MSB\nmsg.payload[10], //11 generator_voltage_31 LSB\nmsg.payload[11], //12 generator_voltage_31 MSB\n\nmsg.payload[20], //13 current_1 LSB\nmsg.payload[21], //14 current_1 MSB\nmsg.payload[22], //15 current_2 LSB\nmsg.payload[23], //16 current_2 MSB\nmsg.payload[24], //17 current_3 LSB\nmsg.payload[25], //18 current_3 MSB\n\nmsg.payload[28], //19 generator_frequency\nmsg.payload[29], //20 busbar_frequency\n\nmsg.payload[60], //21 current_active_power_total LSB\nmsg.payload[61], //22 current_active_power_total MSB\nmsg.payload[62], //23 current_reactive_power_total LSB\nmsg.payload[63], //24 current_reactive_power_total MSB\nmsg.payload[64], //25 current_apparent_power_total LSB\nmsg.payload[65], //26 current_apparent_power_total MSB\n\nmsg.payload[67], //27 current_pf_total\n\nmsg.payload[70], //28 engine_running_hours LSB\nmsg.payload[71], //29 engine_running_hours MSB\n\nmsg.payload[73], //30 engine_battery_voltage\n\nmsg.payload[76], //31 engine_oil_pressure\n\nmsg.payload[77], //32 engine_coolant_temperature LSB\nmsg.payload[78], //33 engine_coolant_temperature MSB\n\nmsg.payload[80], //34 engine_velocity\n\nmsg.payload[85], //35 generator_active_energy LSB\nmsg.payload[86], //36 generator_active_energy MSB\n\nmsg.payload[93], //37 io_cont_voltage_an_input1_JW\nmsg.payload[94]  //38 io_cont_voltage_an_input2_JW\n]};\n\nreturn todos;",
        "outputs": "1",
        "noerr": 0,
        "x": 883.3889083862305,
        "y": 216.2223744392395,
        "wires": [
            [
                "f893240.bcc15e"
            ]
        ]
    },
    {
        "id": "9a50ebc6.8fb938",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Separa Dados",
        "func": "var todos = {payload: [\nmsg.payload[0], //1 - 354 engine_intake_manifold1_press\n//msg.payload[1], //2 - 355\nmsg.payload[2], //3 - 356 engine_throttle_pos\n//msg.payload[3], //4 - 357\n//msg.payload[4], //5 - 358\nmsg.payload[5], //6 - 359 engine_intake_manifold1_temp LSB\nmsg.payload[6], //7 - 360 engine_intake_manifold1_temp MSB\n]};\n\n\nreturn todos;",
        "outputs": "1",
        "noerr": 0,
        "x": 888.1111679077148,
        "y": 262.6111989021301,
        "wires": [
            [
                "81c8a512.5160a8"
            ]
        ]
    },
    {
        "id": "8568d612.5fc9c8",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Separa Dados",
        "func": "var todos = {payload: [\nmsg.payload[0], //1 - 132\n]};\n\nreturn todos;",
        "outputs": "1",
        "noerr": 0,
        "x": 893.1111946105957,
        "y": 304.11124181747437,
        "wires": [
            [
                "85afa925.1477c8"
            ]
        ]
    },
    {
        "id": "85afa925.1477c8",
        "type": "modbus-write",
        "z": "50f61338.29072c",
        "name": "Salva GMG1 Local",
        "showStatusActivities": true,
        "showErrors": true,
        "unitid": "1",
        "dataType": "MHoldingRegisters",
        "adr": "42",
        "quantity": "1",
        "server": "a8d40646.cef038",
        "x": 1119.1112937927246,
        "y": 305.11124181747437,
        "wires": [
            [],
            []
        ]
    },
    {
        "id": "e95609c4.49c0e8",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Separa Dados",
        "func": "var todos = {payload: [\nmsg.payload[0], //1   seconds\nmsg.payload[1], //2   minutes\nmsg.payload[2], //3   hours\nmsg.payload[3], //4   day_of_month\n//msg.payload[4], //5 \nmsg.payload[5], //6   month\nmsg.payload[6], //7   year\n//msg.payload[7], //8 \nmsg.payload[8], //9   engine_running_hours LSB\nmsg.payload[9], //10  engine_running_hours MSB\nmsg.payload[10], //11 number_of_cranks LSB\nmsg.payload[11], //12 number_of_cranks MSB\n//0 a 11 foi\nmsg.payload[24], //13 working_hours_with_load LSB\nmsg.payload[25], //14 working_hours_with_load MSB\n]};\n\n//msg.payload = todos.join();\n//msg.topic=1;\n\nreturn todos;",
        "outputs": "1",
        "noerr": 0,
        "x": 898.1112022399902,
        "y": 350.611243724823,
        "wires": [
            [
                "844eedbd.2782"
            ]
        ]
    },
    {
        "id": "844eedbd.2782",
        "type": "modbus-write",
        "z": "50f61338.29072c",
        "name": "Salva GMG1 Local",
        "showStatusActivities": true,
        "showErrors": true,
        "unitid": "1",
        "dataType": "MHoldingRegisters",
        "adr": "43",
        "quantity": "12",
        "server": "a8d40646.cef038",
        "x": 1119.1589622497559,
        "y": 346.3731360435486,
        "wires": [
            [],
            []
        ]
    },
    {
        "id": "7f407240.c1491c",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Adequa Dados e Razão",
        "func": "var um = 1;\nvar busbar_voltage_12 =  ((msg.payload[1]*65536+msg.payload[0])/256);\nvar busbar_voltage_23 =  ((msg.payload[3]*65536+msg.payload[2])/256);\nvar busbar_voltage_31 =  ((msg.payload[5]*65536+msg.payload[4])/256);\nvar generator_voltage_12 =  ((msg.payload[7]*65536+msg.payload[6])/256);\nvar generator_voltage_23 =  ((msg.payload[9]*65536+msg.payload[8])/256);\nvar generator_voltage_31 =  ((msg.payload[11]*65536+msg.payload[10])/256);\nvar current_1 = ((msg.payload[13]*65536+msg.payload[12])/256);\nvar current_2 =  ((msg.payload[15]*65536+msg.payload[14])/256);\nvar current_3 =  ((msg.payload[17]*65536+msg.payload[16])/256);\nvar generator_frequency =  (msg.payload[18]/256);\nvar busbar_frequency =  (msg.payload[19]/256);\n\nvar current_active_power_total =  ((msg.payload[21]*65536+msg.payload[20])/256);\nif(current_active_power_total>8388607){current_active_power_total=current_active_power_total-16777215;}\n\nvar current_reactive_power_total =  ((msg.payload[23]*65536+msg.payload[22])/256);\nif(current_reactive_power_total>8388607){current_reactive_power_total=current_reactive_power_total-16777215;}\n\nvar current_apparent_power_total =  ((msg.payload[25]*65536+msg.payload[24])/256);\n\nvar current_pf_total =  (msg.payload[26]/256);\nif(current_pf_total>8388607){current_pf_total=current_pf_total-16777215;}\n\n//var engine_running_hours =  ((msg.payload[28]*65536+msg.payload[27]));\nvar engine_battery_voltage =  (msg.payload[29]/256);\nvar engine_oil_pressure =  (msg.payload[30]/256);\nvar engine_coolant_temperature =  ((msg.payload[32]*65536+msg.payload[31])/256);\nvar engine_velocity =  (msg.payload[33]);\nvar generator_active_energy =  ((msg.payload[35]*65536+msg.payload[34]));\nvar io_cont_voltage_an_input1_JW =  (msg.payload[36]/256);\nvar io_cont_voltage_an_input2_JW =  (msg.payload[37]/256);\n//ok 0 a 37 = 38\n\nvar engine_intake_manifold1_press =  (msg.payload[38]*1/256 ); //354\nvar engine_throttle_pos =  (msg.payload[39]*1/256 ); //356\nvar engine_intake_manifold1_temp =  ((msg.payload[41]*65536+msg.payload[40])*1/256 ); //359\n//ok 4\n\nvar engine_status = ((msg.payload[42])); \n//ok 1\n\nvar seconds = ((msg.payload[43])); //1\nvar minutes =  ((msg.payload[44])); //2\nvar hours =  ((msg.payload[45])); //3\nvar day_of_month =  ((msg.payload[46])); //4\nvar month =  ((msg.payload[47]));//5\nvar year =  ((msg.payload[48]));//6\nvar engine_working_hours =  ((msg.payload[50]*65536+msg.payload[49]) );//7-8\nvar number_of_cranks = ((msg.payload[52]*65536+msg.payload[51]) );//9-10\nvar engine_working_hours_with_load = ((msg.payload[54]*65536+msg.payload[53]) );//11-12\n\nvar todos = {payload: [\num,\nbusbar_voltage_12,\nbusbar_voltage_23,\nbusbar_voltage_31,\ngenerator_voltage_12,\ngenerator_voltage_23,\ngenerator_voltage_31,\ncurrent_1,\ncurrent_2,\ncurrent_3,\ngenerator_frequency,\nbusbar_frequency,\ncurrent_active_power_total,\ncurrent_reactive_power_total,\ncurrent_apparent_power_total,\ncurrent_pf_total,\nengine_battery_voltage,\nengine_oil_pressure,\nengine_coolant_temperature,\nengine_velocity,\ngenerator_active_energy,\nio_cont_voltage_an_input1_JW,\nio_cont_voltage_an_input2_JW,\n\nengine_intake_manifold1_press,\nengine_throttle_pos,\nengine_intake_manifold1_temp,\n\nengine_status,\n\nseconds,\nminutes,\nhours,\nday_of_month,\nmonth,\nyear,\nengine_working_hours,\nnumber_of_cranks,\nengine_working_hours_with_load\n]};\n\n\n\nreturn todos;//msg;\n",
        "outputs": "1",
        "noerr": 0,
        "x": 948.7064781188965,
        "y": 412.11133098602295,
        "wires": [
            [
                "26738153.5406ee"
            ]
        ]
    },
    {
        "id": "26738153.5406ee",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "INSERIR NO BANCO DE DADOS",
        "func": "msg.topic =\"SET time_zone='America/Sao_Paulo'; INSERT INTO `dados_brasilgtw`.`dados` (`id_dispositivo`,`busbar_voltage_12`,`busbar_voltage_23`,`busbar_voltage_31`,`generator_voltage_12`,`generator_voltage_23`,`generator_voltage_31`,`current_1`,`current_2`,`current_3`,`generator_frequency`,`busbar_frequency`,`current_active_power_total`,`current_reactive_power_total`,`current_apparent_power_total`,`current_pf_total`,`engine_battery_voltage`,`engine_oil_pressure`,`engine_coolant_temperature`,`engine_velocity`,`generator_active_energy`,`io_cont_voltage_an_input1_JW`,`io_cont_voltage_an_input2_JW`,`engine_intake_manifold1_press`,`engine_throttle_pos`,`engine_intake_manifold1_temp`,`engine_status`,`seconds`,`minutes`,`hours`,`day_of_month`,`month`,`year`,`engine_working_hours`,`number_of_cranks`,`engine_working_hours_with_load`) VALUES (\"+msg.payload+\")\";\n\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 1217.254062652588,
        "y": 406.37313175201416,
        "wires": [
            [
                "2a03d611.26c39a"
            ]
        ]
    },
    {
        "id": "22431e91.b10ff2",
        "type": "catch",
        "z": "50f61338.29072c",
        "name": "",
        "scope": null,
        "x": 370.77769660949707,
        "y": 572.8491444587708,
        "wires": [
            [
                "ff3ae8d2.d97e28"
            ]
        ]
    },
    {
        "id": "b883c50b.226978",
        "type": "modbus-queue-info",
        "z": "50f61338.29072c",
        "name": "Fila Leitura GMG2 Remoto",
        "unitid": "2",
        "lowLowLevel": 25,
        "lowLevel": 75,
        "highLevel": 150,
        "highHighLevel": 300,
        "server": "986a090a.461d98",
        "errorOnHighLevel": false,
        "x": 941.3333034515381,
        "y": 571.6269536018372,
        "wires": [
            [
                "f7ee92a9.8a566"
            ]
        ]
    },
    {
        "id": "ff3ae8d2.d97e28",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Reseta leitura se atingir nivel high high",
        "func": "if(\"high high level reached\" === msg.state && \n    msg.unitid === 2 &&\n    msg.error.source.name === \"Read Queue\") {\n    msg.resetQueue = true;\n    return msg;\n}\n",
        "outputs": 1,
        "noerr": 0,
        "x": 631.1110172271729,
        "y": 569.4046845436096,
        "wires": [
            [
                "b883c50b.226978"
            ]
        ]
    },
    {
        "id": "f7ee92a9.8a566",
        "type": "debug",
        "z": "50f61338.29072c",
        "name": "",
        "active": false,
        "console": "false",
        "complete": "payload",
        "x": 1151.476490020752,
        "y": 570.738018989563,
        "wires": []
    },
    {
        "id": "e140d051.8bd2f",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Lê 1 a 95 (IR)",
        "func": "msg.payload = { input: msg.payload, 'fc': 4, 'unitid': 2, 'address': 0 , 'quantity': 94 }\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 424.3332862854004,
        "y": 631.2778038978577,
        "wires": [
            [
                "d596f41d.0376f8"
            ]
        ]
    },
    {
        "id": "d596f41d.0376f8",
        "type": "modbus-flex-getter",
        "z": "50f61338.29072c",
        "name": "Envia Fila de Leitura GMG2",
        "showStatusActivities": false,
        "showErrors": false,
        "server": "986a090a.461d98",
        "x": 642.8888816833496,
        "y": 637.2777743339539,
        "wires": [
            [
                "d95bce6d.8a09c"
            ],
            []
        ]
    },
    {
        "id": "97dc0246.98ceb",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Lê 354-359 (IR)",
        "func": "msg.payload = { input: msg.payload, 'fc': 4, 'unitid': 2, 'address': 353 , 'quantity': 7 }\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 428.3332633972168,
        "y": 680.2777533531189,
        "wires": [
            [
                "552fda47.07dc54"
            ]
        ]
    },
    {
        "id": "759c092.b3f10f8",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Lê 1-25 (HR)",
        "func": "msg.payload = { input: msg.payload, 'fc': 3, 'unitid': 2, 'address': 0 , 'quantity': 26 }\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 420.5555305480957,
        "y": 776.6111707687378,
        "wires": [
            [
                "1b578d8c.2dd1c2"
            ]
        ]
    },
    {
        "id": "552fda47.07dc54",
        "type": "modbus-flex-getter",
        "z": "50f61338.29072c",
        "name": "Envia Fila de Leitura GMG2",
        "showStatusActivities": false,
        "showErrors": false,
        "server": "986a090a.461d98",
        "x": 645.3332633972168,
        "y": 679.2777533531189,
        "wires": [
            [
                "9f4a485f.7d5ab8"
            ],
            []
        ]
    },
    {
        "id": "1b578d8c.2dd1c2",
        "type": "modbus-flex-getter",
        "z": "50f61338.29072c",
        "name": "Envia Fila de Leitura GMG2",
        "showStatusActivities": false,
        "showErrors": false,
        "server": "986a090a.461d98",
        "x": 648.5555229187012,
        "y": 772.6111254692078,
        "wires": [
            [
                "b190f228.5282e"
            ],
            []
        ]
    },
    {
        "id": "b543aa59.5ce0d8",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Lê 132 (IR)",
        "func": "msg.payload = { input: msg.payload, 'fc': 4, 'unitid': 2, 'address': 131 , 'quantity': 1 }\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 412.66657638549805,
        "y": 726.6110663414001,
        "wires": [
            [
                "1176aa5.a4b5c56"
            ]
        ]
    },
    {
        "id": "1176aa5.a4b5c56",
        "type": "modbus-flex-getter",
        "z": "50f61338.29072c",
        "name": "Envia Fila de Leitura GMG2",
        "showStatusActivities": false,
        "showErrors": false,
        "server": "986a090a.461d98",
        "x": 639.666576385498,
        "y": 725.6110663414001,
        "wires": [
            [
                "ac6fa40e.ac9e88"
            ],
            []
        ]
    },
    {
        "id": "a215863c.70b358",
        "type": "modbus-write",
        "z": "50f61338.29072c",
        "name": "Salva GMG2 Local",
        "showStatusActivities": true,
        "showErrors": true,
        "unitid": "1",
        "dataType": "MHoldingRegisters",
        "adr": "55",
        "quantity": "38",
        "server": "a8d40646.cef038",
        "x": 1110.7777214050293,
        "y": 634.9445562362671,
        "wires": [
            [],
            []
        ]
    },
    {
        "id": "9dd7493d.5d2b08",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Lê GMG2 local",
        "func": "msg.payload = { input: msg.payload, 'fc': 3, 'unitid': 1, 'address': 55 , 'quantity': 55 }\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 449.7619972229004,
        "y": 821.5159864425659,
        "wires": [
            [
                "a5651f1a.16556"
            ]
        ]
    },
    {
        "id": "a5651f1a.16556",
        "type": "modbus-flex-getter",
        "z": "50f61338.29072c",
        "name": "Envia Fila de Leitura GMG2 Local",
        "showStatusActivities": false,
        "showErrors": false,
        "server": "a8d40646.cef038",
        "x": 689.6348495483398,
        "y": 823.738175868988,
        "wires": [
            [
                "365eab52.0189c4"
            ],
            []
        ]
    },
    {
        "id": "e6e2f5b4.42c238",
        "type": "modbus-write",
        "z": "50f61338.29072c",
        "name": "Salva GMG2 Local",
        "showStatusActivities": true,
        "showErrors": true,
        "unitid": "1",
        "dataType": "MHoldingRegisters",
        "adr": "93",
        "quantity": "4",
        "server": "a8d40646.cef038",
        "x": 1106.6907272338867,
        "y": 680.0081572532654,
        "wires": [
            [],
            []
        ]
    },
    {
        "id": "d95bce6d.8a09c",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Separa Dados",
        "func": "var todos = {payload: [\nmsg.payload[0], //1   busbar_voltage_12 LSB\nmsg.payload[1], //2   busbar_voltage_12 MSB\nmsg.payload[2], //3   busbar_voltage_23 LSB\nmsg.payload[3], //4   busbar_voltage_23 MSB\nmsg.payload[4], //5   busbar_voltage_31 LSB\nmsg.payload[5], //6   busbar_voltage_31 MSB\nmsg.payload[6], //7   generator_voltage_12 LSB\nmsg.payload[7], //8   generator_voltage_12 MSB\nmsg.payload[8], //9   generator_voltage_23 LSB\nmsg.payload[9], //10  generator_voltage_23 MSB\nmsg.payload[10], //11 generator_voltage_31 LSB\nmsg.payload[11], //12 generator_voltage_31 MSB\n\nmsg.payload[20], //13 current_1 LSB\nmsg.payload[21], //14 current_1 MSB\nmsg.payload[22], //15 current_2 LSB\nmsg.payload[23], //16 current_2 MSB\nmsg.payload[24], //17 current_3 LSB\nmsg.payload[25], //18 current_3 MSB\n\nmsg.payload[28], //19 generator_frequency\nmsg.payload[29], //20 busbar_frequency\n\nmsg.payload[60], //21 current_active_power_total LSB\nmsg.payload[61], //22 current_active_power_total MSB\nmsg.payload[62], //23 current_reactive_power_total LSB\nmsg.payload[63], //24 current_reactive_power_total MSB\nmsg.payload[64], //25 current_apparent_power_total LSB\nmsg.payload[65], //26 current_apparent_power_total MSB\n\nmsg.payload[67], //27 current_pf_total\n\nmsg.payload[70], //28 engine_running_hours LSB\nmsg.payload[71], //29 engine_running_hours MSB\n\nmsg.payload[73], //30 engine_battery_voltage\n\nmsg.payload[76], //31 engine_oil_pressure\n\nmsg.payload[77], //32 engine_coolant_temperature LSB\nmsg.payload[78], //33 engine_coolant_temperature MSB\n\nmsg.payload[80], //34 engine_velocity\n\nmsg.payload[85], //35 generator_active_energy LSB\nmsg.payload[86], //36 generator_active_energy MSB\n\nmsg.payload[93], //37 io_cont_voltage_an_input1_JW\nmsg.payload[94]  //38 io_cont_voltage_an_input2_JW\n]};\n\nreturn todos;",
        "outputs": "1",
        "noerr": 0,
        "x": 872.2777519226074,
        "y": 634.2224011421204,
        "wires": [
            [
                "a215863c.70b358"
            ]
        ]
    },
    {
        "id": "9f4a485f.7d5ab8",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Separa Dados",
        "func": "var todos = {payload: [\nmsg.payload[0], //1 - 354 engine_intake_manifold1_press\n//msg.payload[1], //2 - 355\nmsg.payload[2], //3 - 356 engine_throttle_pos\n//msg.payload[3], //4 - 357\n//msg.payload[4], //5 - 358\nmsg.payload[5], //6 - 359 engine_intake_manifold1_temp LSB\nmsg.payload[6], //7 - 360 engine_intake_manifold1_temp MSB\n]};\n\n\nreturn todos;",
        "outputs": "1",
        "noerr": 0,
        "x": 877.0000114440918,
        "y": 680.611225605011,
        "wires": [
            [
                "e6e2f5b4.42c238"
            ]
        ]
    },
    {
        "id": "ac6fa40e.ac9e88",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Separa Dados",
        "func": "var todos = {payload: [\nmsg.payload[0], //1 - 132\n]};\n\nreturn todos;",
        "outputs": "1",
        "noerr": 0,
        "x": 882.0000381469727,
        "y": 722.1112685203552,
        "wires": [
            [
                "48047abb.922894"
            ]
        ]
    },
    {
        "id": "48047abb.922894",
        "type": "modbus-write",
        "z": "50f61338.29072c",
        "name": "Salva GMG2 Local",
        "showStatusActivities": true,
        "showErrors": true,
        "unitid": "1",
        "dataType": "MHoldingRegisters",
        "adr": "97",
        "quantity": "1",
        "server": "a8d40646.cef038",
        "x": 1104.000415802002,
        "y": 723.111305296421,
        "wires": [
            [],
            []
        ]
    },
    {
        "id": "b190f228.5282e",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Separa Dados",
        "func": "var todos = {payload: [\nmsg.payload[0], //1   seconds\nmsg.payload[1], //2   minutes\nmsg.payload[2], //3   hours\nmsg.payload[3], //4   day_of_month\n//msg.payload[4], //5 \nmsg.payload[5], //6   month\nmsg.payload[6], //7   year\n//msg.payload[7], //8 \nmsg.payload[8], //9   engine_running_hours LSB\nmsg.payload[9], //10  engine_running_hours MSB\nmsg.payload[10], //11 number_of_cranks LSB\nmsg.payload[11], //12 number_of_cranks MSB\n//0 a 11 foi\nmsg.payload[24], //13 working_hours_with_load LSB\nmsg.payload[25], //14 working_hours_with_load MSB\n]};\n\n//msg.payload = todos.join();\n//msg.topic=1;\n\nreturn todos;",
        "outputs": "1",
        "noerr": 0,
        "x": 887.0000457763672,
        "y": 768.6112704277039,
        "wires": [
            [
                "4f2993f3.ede01c"
            ]
        ]
    },
    {
        "id": "4f2993f3.ede01c",
        "type": "modbus-write",
        "z": "50f61338.29072c",
        "name": "Salva GMG2 Local",
        "showStatusActivities": true,
        "showErrors": true,
        "unitid": "1",
        "dataType": "MHoldingRegisters",
        "adr": "98",
        "quantity": "12",
        "server": "a8d40646.cef038",
        "x": 1108.0478057861328,
        "y": 764.3731627464294,
        "wires": [
            [],
            []
        ]
    },
    {
        "id": "365eab52.0189c4",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Adequa Dados e Razão",
        "func": "var dois = 2;\nvar busbar_voltage_12 =  ((msg.payload[1]*65536+msg.payload[0])/256);\nvar busbar_voltage_23 =  ((msg.payload[3]*65536+msg.payload[2])/256);\nvar busbar_voltage_31 =  ((msg.payload[5]*65536+msg.payload[4])/256);\nvar generator_voltage_12 =  ((msg.payload[7]*65536+msg.payload[6])/256);\nvar generator_voltage_23 =  ((msg.payload[9]*65536+msg.payload[8])/256);\nvar generator_voltage_31 =  ((msg.payload[11]*65536+msg.payload[10])/256);\nvar current_1 = ((msg.payload[13]*65536+msg.payload[12])/256);\nvar current_2 =  ((msg.payload[15]*65536+msg.payload[14])/256);\nvar current_3 =  ((msg.payload[17]*65536+msg.payload[16])/256);\nvar generator_frequency =  (msg.payload[18]/256);\nvar busbar_frequency =  (msg.payload[19]/256);\n\nvar current_active_power_total =  ((msg.payload[21]*65536+msg.payload[20])/256);\nif(current_active_power_total>8388607){current_active_power_total=current_active_power_total-16777215;}\n\nvar current_reactive_power_total =  ((msg.payload[23]*65536+msg.payload[22])/256);\nif(current_reactive_power_total>8388607){current_reactive_power_total=current_reactive_power_total-16777215;}\n\nvar current_apparent_power_total =  ((msg.payload[25]*65536+msg.payload[24])/256);\n\nvar current_pf_total =  (msg.payload[26]/256);\nif(current_pf_total>8388607){current_pf_total=current_pf_total-16777215;}\n\n//var engine_running_hours =  ((msg.payload[28]*65536+msg.payload[27]));\nvar engine_battery_voltage =  (msg.payload[29]/256);\nvar engine_oil_pressure =  (msg.payload[30]/256);\nvar engine_coolant_temperature =  ((msg.payload[32]*65536+msg.payload[31])/256);\nvar engine_velocity =  (msg.payload[33]);\nvar generator_active_energy =  ((msg.payload[35]*65536+msg.payload[34]));\nvar io_cont_voltage_an_input1_JW =  (msg.payload[36]/256);\nvar io_cont_voltage_an_input2_JW =  (msg.payload[37]/256);\n//ok 0 a 37 = 38\n\nvar engine_intake_manifold1_press =  (msg.payload[38]*1/256 ); //354\nvar engine_throttle_pos =  (msg.payload[39]*1/256 ); //356\nvar engine_intake_manifold1_temp =  ((msg.payload[41]*65536+msg.payload[40])*1/256 ); //359\n//ok 4\n\nvar engine_status = ((msg.payload[42])); \n//ok 1\n\nvar seconds = ((msg.payload[43])); //1\nvar minutes =  ((msg.payload[44])); //2\nvar hours =  ((msg.payload[45])); //3\nvar day_of_month =  ((msg.payload[46])); //4\nvar month =  ((msg.payload[47]));//5\nvar year =  ((msg.payload[48]));//6\nvar engine_working_hours =  ((msg.payload[50]*65536+msg.payload[49]) );//7-8\nvar number_of_cranks = ((msg.payload[52]*65536+msg.payload[51]) );//9-10\nvar engine_working_hours_with_load = ((msg.payload[54]*65536+msg.payload[53]) );//11-12\n\nvar todos = {payload: [\ndois,\nbusbar_voltage_12,\nbusbar_voltage_23,\nbusbar_voltage_31,\ngenerator_voltage_12,\ngenerator_voltage_23,\ngenerator_voltage_31,\ncurrent_1,\ncurrent_2,\ncurrent_3,\ngenerator_frequency,\nbusbar_frequency,\ncurrent_active_power_total,\ncurrent_reactive_power_total,\ncurrent_apparent_power_total,\ncurrent_pf_total,\nengine_battery_voltage,\nengine_oil_pressure,\nengine_coolant_temperature,\nengine_velocity,\ngenerator_active_energy,\nio_cont_voltage_an_input1_JW,\nio_cont_voltage_an_input2_JW,\n\nengine_intake_manifold1_press,\nengine_throttle_pos,\nengine_intake_manifold1_temp,\n\nengine_status,\n\nseconds,\nminutes,\nhours,\nday_of_month,\nmonth,\nyear,\nengine_working_hours,\nnumber_of_cranks,\nengine_working_hours_with_load\n]};\n\n\n\nreturn todos;//msg;\n",
        "outputs": "1",
        "noerr": 0,
        "x": 963.3809852600098,
        "y": 825.0399713516235,
        "wires": [
            [
                "635a972b.8dda68"
            ]
        ]
    },
    {
        "id": "635a972b.8dda68",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "INSERIR NO BANCO DE DADOS",
        "func": "msg.topic =\"SET time_zone='America/Sao_Paulo'; INSERT INTO `dados_brasilgtw`.`dados` (`id_dispositivo`,`busbar_voltage_12`,`busbar_voltage_23`,`busbar_voltage_31`,`generator_voltage_12`,`generator_voltage_23`,`generator_voltage_31`,`current_1`,`current_2`,`current_3`,`generator_frequency`,`busbar_frequency`,`current_active_power_total`,`current_reactive_power_total`,`current_apparent_power_total`,`current_pf_total`,`engine_battery_voltage`,`engine_oil_pressure`,`engine_coolant_temperature`,`engine_velocity`,`generator_active_energy`,`io_cont_voltage_an_input1_JW`,`io_cont_voltage_an_input2_JW`,`engine_intake_manifold1_press`,`engine_throttle_pos`,`engine_intake_manifold1_temp`,`engine_status`,`seconds`,`minutes`,`hours`,`day_of_month`,`month`,`year`,`engine_working_hours`,`number_of_cranks`,`engine_working_hours_with_load`) VALUES (\"+msg.payload+\")\";\n\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 1251.095401763916,
        "y": 818.9127292633057,
        "wires": [
            [
                "2a03d611.26c39a"
            ]
        ]
    },
    {
        "id": "733e8745.b77128",
        "type": "delay",
        "z": "50f61338.29072c",
        "name": "",
        "pauseType": "delay",
        "timeout": "1",
        "timeoutUnits": "milliseconds",
        "rate": "1",
        "nbRateUnits": "1",
        "rateUnits": "second",
        "randomFirst": "1",
        "randomLast": "5",
        "randomUnits": "seconds",
        "drop": false,
        "x": 177.2221221923828,
        "y": 725.055567741394,
        "wires": [
            [
                "e140d051.8bd2f",
                "97dc0246.98ceb",
                "b543aa59.5ce0d8",
                "759c092.b3f10f8",
                "9dd7493d.5d2b08"
            ]
        ]
    },
    {
        "id": "6f33277a.a29cd8",
        "type": "catch",
        "z": "50f61338.29072c",
        "name": "",
        "scope": null,
        "x": 397.85720443725586,
        "y": 1001.4920416474342,
        "wires": [
            [
                "3cae385e.298fa8"
            ]
        ]
    },
    {
        "id": "dcfcfbbf.4b87d8",
        "type": "modbus-queue-info",
        "z": "50f61338.29072c",
        "name": "Fila Leitura GMG3 Remoto",
        "unitid": "3",
        "lowLowLevel": 25,
        "lowLevel": 75,
        "highLevel": 150,
        "highHighLevel": 300,
        "server": "986a090a.461d98",
        "errorOnHighLevel": false,
        "x": 966.7461585998535,
        "y": 1001.9365130066872,
        "wires": [
            [
                "e8fc00eb.b7d"
            ]
        ]
    },
    {
        "id": "3cae385e.298fa8",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Reseta leitura se atingir nivel high high",
        "func": "if(\"high high level reached\" === msg.state && \n    msg.unitid === 3 &&\n    msg.error.source.name === \"Read Queue\") {\n    msg.resetQueue = true;\n    return msg;\n}\n",
        "outputs": 1,
        "noerr": 0,
        "x": 659.857177734375,
        "y": 1003.0475967526436,
        "wires": [
            [
                "dcfcfbbf.4b87d8"
            ]
        ]
    },
    {
        "id": "e8fc00eb.b7d",
        "type": "debug",
        "z": "50f61338.29072c",
        "name": "",
        "active": false,
        "console": "false",
        "complete": "payload",
        "x": 1211.8892517089844,
        "y": 999.380978167057,
        "wires": []
    },
    {
        "id": "8f3ee414.0fbb48",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Lê 1 a 95 (IR)",
        "func": "msg.payload = { input: msg.payload, 'fc': 4, 'unitid': 3, 'address': 0 , 'quantity': 94 }\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 413.07947540283203,
        "y": 1056.587372303009,
        "wires": [
            [
                "16d6b7e8.664978"
            ]
        ]
    },
    {
        "id": "16d6b7e8.664978",
        "type": "modbus-flex-getter",
        "z": "50f61338.29072c",
        "name": "Envia Fila de Leitura GMG3",
        "showStatusActivities": false,
        "showErrors": false,
        "server": "986a090a.461d98",
        "x": 631.6350708007812,
        "y": 1062.5873427391052,
        "wires": [
            [
                "eb26911c.e1b1e"
            ],
            []
        ]
    },
    {
        "id": "2c39ad46.6b4982",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Lê 354-359 (IR)",
        "func": "msg.payload = { input: msg.payload, 'fc': 4, 'unitid': 3, 'address': 353 , 'quantity': 7 }\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 417.07945251464844,
        "y": 1105.5873217582703,
        "wires": [
            [
                "2ed56c52.6f1834"
            ]
        ]
    },
    {
        "id": "81b58cdc.5d73f",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Lê 1-25 (HR)",
        "func": "msg.payload = { input: msg.payload, 'fc': 3, 'unitid': 3, 'address': 0 , 'quantity': 26 }\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 409.30171966552734,
        "y": 1201.9207391738892,
        "wires": [
            [
                "3ec74125.4585ce"
            ]
        ]
    },
    {
        "id": "2ed56c52.6f1834",
        "type": "modbus-flex-getter",
        "z": "50f61338.29072c",
        "name": "Envia Fila de Leitura GMG3",
        "showStatusActivities": false,
        "showErrors": false,
        "server": "986a090a.461d98",
        "x": 634.0794525146484,
        "y": 1104.5873217582703,
        "wires": [
            [
                "83e342a6.f4339"
            ],
            []
        ]
    },
    {
        "id": "3ec74125.4585ce",
        "type": "modbus-flex-getter",
        "z": "50f61338.29072c",
        "name": "Envia Fila de Leitura GMG3",
        "showStatusActivities": false,
        "showErrors": false,
        "server": "986a090a.461d98",
        "x": 637.3017120361328,
        "y": 1197.9206938743591,
        "wires": [
            [
                "ccd38280.11c83"
            ],
            []
        ]
    },
    {
        "id": "c41a1d8a.af163",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Lê 132 (IR)",
        "func": "msg.payload = { input: msg.payload, 'fc': 4, 'unitid': 3, 'address': 131 , 'quantity': 1 }\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 401.4127655029297,
        "y": 1151.9206347465515,
        "wires": [
            [
                "6a85ca03.3f12e4"
            ]
        ]
    },
    {
        "id": "6a85ca03.3f12e4",
        "type": "modbus-flex-getter",
        "z": "50f61338.29072c",
        "name": "Envia Fila de Leitura GMG3",
        "showStatusActivities": false,
        "showErrors": false,
        "server": "986a090a.461d98",
        "x": 628.4127655029297,
        "y": 1150.9206347465515,
        "wires": [
            [
                "3278c2ce.e9a95e"
            ],
            []
        ]
    },
    {
        "id": "d240a7ef.437998",
        "type": "modbus-write",
        "z": "50f61338.29072c",
        "name": "Salva GMG3 Local",
        "showStatusActivities": true,
        "showErrors": true,
        "unitid": "1",
        "dataType": "MHoldingRegisters",
        "adr": "110",
        "quantity": "38",
        "server": "a8d40646.cef038",
        "x": 1099.523910522461,
        "y": 1060.2541246414185,
        "wires": [
            [],
            []
        ]
    },
    {
        "id": "47e8fdd0.f9e504",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Lê GMG3 local",
        "func": "msg.payload = { input: msg.payload, 'fc': 3, 'unitid': 3, 'address': 110 , 'quantity': 55 }\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 438.50818634033203,
        "y": 1246.8255548477173,
        "wires": [
            [
                "c8bc863f.50eaa8"
            ]
        ]
    },
    {
        "id": "c8bc863f.50eaa8",
        "type": "modbus-flex-getter",
        "z": "50f61338.29072c",
        "name": "Envia Fila de Leitura GMG3 Local",
        "showStatusActivities": false,
        "showErrors": false,
        "server": "a8d40646.cef038",
        "x": 678.3810386657715,
        "y": 1249.0477442741394,
        "wires": [
            [
                "c23efdad.47236"
            ],
            []
        ]
    },
    {
        "id": "3dc57b8a.17cbf4",
        "type": "modbus-write",
        "z": "50f61338.29072c",
        "name": "Salva GMG3 Local",
        "showStatusActivities": true,
        "showErrors": true,
        "unitid": "1",
        "dataType": "MHoldingRegisters",
        "adr": "148",
        "quantity": "4",
        "server": "a8d40646.cef038",
        "x": 1095.4369163513184,
        "y": 1105.3177256584167,
        "wires": [
            [],
            []
        ]
    },
    {
        "id": "eb26911c.e1b1e",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Separa Dados",
        "func": "var todos = {payload: [\nmsg.payload[0], //1   busbar_voltage_12 LSB\nmsg.payload[1], //2   busbar_voltage_12 MSB\nmsg.payload[2], //3   busbar_voltage_23 LSB\nmsg.payload[3], //4   busbar_voltage_23 MSB\nmsg.payload[4], //5   busbar_voltage_31 LSB\nmsg.payload[5], //6   busbar_voltage_31 MSB\nmsg.payload[6], //7   generator_voltage_12 LSB\nmsg.payload[7], //8   generator_voltage_12 MSB\nmsg.payload[8], //9   generator_voltage_23 LSB\nmsg.payload[9], //10  generator_voltage_23 MSB\nmsg.payload[10], //11 generator_voltage_31 LSB\nmsg.payload[11], //12 generator_voltage_31 MSB\n\nmsg.payload[20], //13 current_1 LSB\nmsg.payload[21], //14 current_1 MSB\nmsg.payload[22], //15 current_2 LSB\nmsg.payload[23], //16 current_2 MSB\nmsg.payload[24], //17 current_3 LSB\nmsg.payload[25], //18 current_3 MSB\n\nmsg.payload[28], //19 generator_frequency\nmsg.payload[29], //20 busbar_frequency\n\nmsg.payload[60], //21 current_active_power_total LSB\nmsg.payload[61], //22 current_active_power_total MSB\nmsg.payload[62], //23 current_reactive_power_total LSB\nmsg.payload[63], //24 current_reactive_power_total MSB\nmsg.payload[64], //25 current_apparent_power_total LSB\nmsg.payload[65], //26 current_apparent_power_total MSB\n\nmsg.payload[67], //27 current_pf_total\n\nmsg.payload[70], //28 engine_running_hours LSB\nmsg.payload[71], //29 engine_running_hours MSB\n\nmsg.payload[73], //30 engine_battery_voltage\n\nmsg.payload[76], //31 engine_oil_pressure\n\nmsg.payload[77], //32 engine_coolant_temperature LSB\nmsg.payload[78], //33 engine_coolant_temperature MSB\n\nmsg.payload[80], //34 engine_velocity\n\nmsg.payload[85], //35 generator_active_energy LSB\nmsg.payload[86], //36 generator_active_energy MSB\n\nmsg.payload[93], //37 io_cont_voltage_an_input1_JW\nmsg.payload[94]  //38 io_cont_voltage_an_input2_JW\n]};\n\nreturn todos;",
        "outputs": "1",
        "noerr": 0,
        "x": 861.0239410400391,
        "y": 1059.5319695472717,
        "wires": [
            [
                "d240a7ef.437998"
            ]
        ]
    },
    {
        "id": "83e342a6.f4339",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Separa Dados",
        "func": "var todos = {payload: [\nmsg.payload[0], //1 - 354 engine_intake_manifold1_press\n//msg.payload[1], //2 - 355\nmsg.payload[2], //3 - 356 engine_throttle_pos\n//msg.payload[3], //4 - 357\n//msg.payload[4], //5 - 358\nmsg.payload[5], //6 - 359 engine_intake_manifold1_temp LSB\nmsg.payload[6], //7 - 360 engine_intake_manifold1_temp MSB\n]};\n\n\nreturn todos;",
        "outputs": "1",
        "noerr": 0,
        "x": 865.7462005615234,
        "y": 1105.9207940101624,
        "wires": [
            [
                "3dc57b8a.17cbf4"
            ]
        ]
    },
    {
        "id": "3278c2ce.e9a95e",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Separa Dados",
        "func": "var todos = {payload: [\nmsg.payload[0], //1 - 132\n]};\n\nreturn todos;",
        "outputs": "1",
        "noerr": 0,
        "x": 870.7462272644043,
        "y": 1147.4208369255066,
        "wires": [
            [
                "c265e220.41e0a"
            ]
        ]
    },
    {
        "id": "c265e220.41e0a",
        "type": "modbus-write",
        "z": "50f61338.29072c",
        "name": "Salva GMG3 Local",
        "showStatusActivities": true,
        "showErrors": true,
        "unitid": "1",
        "dataType": "MHoldingRegisters",
        "adr": "152",
        "quantity": "1",
        "server": "a8d40646.cef038",
        "x": 1092.7466049194336,
        "y": 1148.4208737015724,
        "wires": [
            [],
            []
        ]
    },
    {
        "id": "ccd38280.11c83",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Separa Dados",
        "func": "var todos = {payload: [\nmsg.payload[0], //1   seconds\nmsg.payload[1], //2   minutes\nmsg.payload[2], //3   hours\nmsg.payload[3], //4   day_of_month\n//msg.payload[4], //5 \nmsg.payload[5], //6   month\nmsg.payload[6], //7   year\n//msg.payload[7], //8 \nmsg.payload[8], //9   engine_running_hours LSB\nmsg.payload[9], //10  engine_running_hours MSB\nmsg.payload[10], //11 number_of_cranks LSB\nmsg.payload[11], //12 number_of_cranks MSB\n//0 a 11 foi\nmsg.payload[24], //13 working_hours_with_load LSB\nmsg.payload[25], //14 working_hours_with_load MSB\n]};\n\n//msg.payload = todos.join();\n//msg.topic=1;\n\nreturn todos;",
        "outputs": "1",
        "noerr": 0,
        "x": 875.7462348937988,
        "y": 1193.9208388328552,
        "wires": [
            [
                "b69df1b5.a29f7"
            ]
        ]
    },
    {
        "id": "b69df1b5.a29f7",
        "type": "modbus-write",
        "z": "50f61338.29072c",
        "name": "Salva GMG3 Local",
        "showStatusActivities": true,
        "showErrors": true,
        "unitid": "1",
        "dataType": "MHoldingRegisters",
        "adr": "153",
        "quantity": "12",
        "server": "a8d40646.cef038",
        "x": 1096.7939949035645,
        "y": 1189.6827311515808,
        "wires": [
            [],
            []
        ]
    },
    {
        "id": "c23efdad.47236",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Adequa Dados e Razão",
        "func": "var tres = 3;\nvar busbar_voltage_12 =  ((msg.payload[1]*65536+msg.payload[0])/256);\nvar busbar_voltage_23 =  ((msg.payload[3]*65536+msg.payload[2])/256);\nvar busbar_voltage_31 =  ((msg.payload[5]*65536+msg.payload[4])/256);\nvar generator_voltage_12 =  ((msg.payload[7]*65536+msg.payload[6])/256);\nvar generator_voltage_23 =  ((msg.payload[9]*65536+msg.payload[8])/256);\nvar generator_voltage_31 =  ((msg.payload[11]*65536+msg.payload[10])/256);\nvar current_1 = ((msg.payload[13]*65536+msg.payload[12])/256);\nvar current_2 =  ((msg.payload[15]*65536+msg.payload[14])/256);\nvar current_3 =  ((msg.payload[17]*65536+msg.payload[16])/256);\nvar generator_frequency =  (msg.payload[18]/256);\nvar busbar_frequency =  (msg.payload[19]/256);\n\nvar current_active_power_total =  ((msg.payload[21]*65536+msg.payload[20])/256);\nif(current_active_power_total>8388607){current_active_power_total=current_active_power_total-16777215;}\n\nvar current_reactive_power_total =  ((msg.payload[23]*65536+msg.payload[22])/256);\nif(current_reactive_power_total>8388607){current_reactive_power_total=current_reactive_power_total-16777215;}\n\nvar current_apparent_power_total =  ((msg.payload[25]*65536+msg.payload[24])/256);\n\nvar current_pf_total =  (msg.payload[26]/256);\nif(current_pf_total>8388607){current_pf_total=current_pf_total-16777215;}\n\n//var engine_running_hours =  ((msg.payload[28]*65536+msg.payload[27]));\nvar engine_battery_voltage =  (msg.payload[29]/256);\nvar engine_oil_pressure =  (msg.payload[30]/256);\nvar engine_coolant_temperature =  ((msg.payload[32]*65536+msg.payload[31])/256);\nvar engine_velocity =  (msg.payload[33]);\nvar generator_active_energy =  ((msg.payload[35]*65536+msg.payload[34]));\nvar io_cont_voltage_an_input1_JW =  (msg.payload[36]/256);\nvar io_cont_voltage_an_input2_JW =  (msg.payload[37]/256);\n//ok 0 a 37 = 38\n\nvar engine_intake_manifold1_press =  (msg.payload[38]*1/256 ); //354\nvar engine_throttle_pos =  (msg.payload[39]*1/256 ); //356\nvar engine_intake_manifold1_temp =  ((msg.payload[41]*65536+msg.payload[40])*1/256 ); //359\n//ok 4\n\nvar engine_status = ((msg.payload[42])); \n//ok 1\n\nvar seconds = ((msg.payload[43])); //1\nvar minutes =  ((msg.payload[44])); //2\nvar hours =  ((msg.payload[45])); //3\nvar day_of_month =  ((msg.payload[46])); //4\nvar month =  ((msg.payload[47]));//5\nvar year =  ((msg.payload[48]));//6\nvar engine_working_hours =  ((msg.payload[50]*65536+msg.payload[49]) );//7-8\nvar number_of_cranks = ((msg.payload[52]*65536+msg.payload[51]) );//9-10\nvar engine_working_hours_with_load = ((msg.payload[54]*65536+msg.payload[53]) );//11-12\n\nvar todos = {payload: [\ntres,\nbusbar_voltage_12,\nbusbar_voltage_23,\nbusbar_voltage_31,\ngenerator_voltage_12,\ngenerator_voltage_23,\ngenerator_voltage_31,\ncurrent_1,\ncurrent_2,\ncurrent_3,\ngenerator_frequency,\nbusbar_frequency,\ncurrent_active_power_total,\ncurrent_reactive_power_total,\ncurrent_apparent_power_total,\ncurrent_pf_total,\nengine_battery_voltage,\nengine_oil_pressure,\nengine_coolant_temperature,\nengine_velocity,\ngenerator_active_energy,\nio_cont_voltage_an_input1_JW,\nio_cont_voltage_an_input2_JW,\n\nengine_intake_manifold1_press,\nengine_throttle_pos,\nengine_intake_manifold1_temp,\n\nengine_status,\n\nseconds,\nminutes,\nhours,\nday_of_month,\nmonth,\nyear,\nengine_working_hours,\nnumber_of_cranks,\nengine_working_hours_with_load\n]};\n\n\n\nreturn todos;//msg;\n",
        "outputs": "1",
        "noerr": 0,
        "x": 952.1271743774414,
        "y": 1250.349539756775,
        "wires": [
            [
                "41dc488c.c51ee8"
            ]
        ]
    },
    {
        "id": "41dc488c.c51ee8",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "INSERIR NO BANCO DE DADOS",
        "func": "msg.topic =\"SET time_zone='America/Sao_Paulo'; INSERT INTO `dados_brasilgtw`.`dados` (`id_dispositivo`,`busbar_voltage_12`,`busbar_voltage_23`,`busbar_voltage_31`,`generator_voltage_12`,`generator_voltage_23`,`generator_voltage_31`,`current_1`,`current_2`,`current_3`,`generator_frequency`,`busbar_frequency`,`current_active_power_total`,`current_reactive_power_total`,`current_apparent_power_total`,`current_pf_total`,`engine_battery_voltage`,`engine_oil_pressure`,`engine_coolant_temperature`,`engine_velocity`,`generator_active_energy`,`io_cont_voltage_an_input1_JW`,`io_cont_voltage_an_input2_JW`,`engine_intake_manifold1_press`,`engine_throttle_pos`,`engine_intake_manifold1_temp`,`engine_status`,`seconds`,`minutes`,`hours`,`day_of_month`,`month`,`year`,`engine_working_hours`,`number_of_cranks`,`engine_working_hours_with_load`) VALUES (\"+msg.payload+\")\";\n\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 1239.8415908813477,
        "y": 1244.222297668457,
        "wires": [
            [
                "2a03d611.26c39a"
            ]
        ]
    },
    {
        "id": "2188c9c2.00f9c6",
        "type": "delay",
        "z": "50f61338.29072c",
        "name": "",
        "pauseType": "delay",
        "timeout": "1",
        "timeoutUnits": "milliseconds",
        "rate": "1",
        "nbRateUnits": "1",
        "rateUnits": "second",
        "randomFirst": "1",
        "randomLast": "5",
        "randomUnits": "seconds",
        "drop": false,
        "x": 194.3016357421875,
        "y": 1137.0318622589111,
        "wires": [
            [
                "8f3ee414.0fbb48",
                "2c39ad46.6b4982",
                "c41a1d8a.af163",
                "81b58cdc.5d73f",
                "47e8fdd0.f9e504"
            ]
        ]
    },
    {
        "id": "69428fbe.33783",
        "type": "catch",
        "z": "50f61338.29072c",
        "name": "",
        "scope": null,
        "x": 413.5714302062988,
        "y": 1413.3968319892883,
        "wires": [
            [
                "a4083c3a.f6fef"
            ]
        ]
    },
    {
        "id": "246952b5.18832e",
        "type": "modbus-queue-info",
        "z": "50f61338.29072c",
        "name": "Fila Leitura GMG4 Remoto",
        "unitid": "4",
        "lowLowLevel": 25,
        "lowLevel": 75,
        "highLevel": 150,
        "highHighLevel": 300,
        "server": "986a090a.461d98",
        "errorOnHighLevel": false,
        "x": 990.7937316894531,
        "y": 1407.1746573448181,
        "wires": [
            [
                "9f10384a.eb5d48"
            ]
        ]
    },
    {
        "id": "a4083c3a.f6fef",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Reseta leitura se atingir nivel high high",
        "func": "if(\"high high level reached\" === msg.state && \n    msg.unitid === 4 &&\n    msg.error.source.name === \"Read Queue\") {\n    msg.resetQueue = true;\n    return msg;\n}\n",
        "outputs": 1,
        "noerr": 0,
        "x": 673.9048004150391,
        "y": 1411.6190733909607,
        "wires": [
            [
                "246952b5.18832e"
            ]
        ]
    },
    {
        "id": "9f10384a.eb5d48",
        "type": "debug",
        "z": "50f61338.29072c",
        "name": "",
        "active": false,
        "console": "false",
        "complete": "payload",
        "x": 1227.6034727096558,
        "y": 1407.9524068832397,
        "wires": []
    },
    {
        "id": "abd8f923.456568",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Lê 1 a 95 (IR)",
        "func": "msg.payload = { input: msg.payload, 'fc': 4, 'unitid': 4, 'address': 0 , 'quantity': 94 }\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 428.7937698364258,
        "y": 1465.1588444709778,
        "wires": [
            [
                "a1dbd722.ff7d08"
            ]
        ]
    },
    {
        "id": "a1dbd722.ff7d08",
        "type": "modbus-flex-getter",
        "z": "50f61338.29072c",
        "name": "Envia Fila de Leitura GMG4",
        "showStatusActivities": false,
        "showErrors": false,
        "server": "986a090a.461d98",
        "x": 647.349365234375,
        "y": 1471.158814907074,
        "wires": [
            [
                "7b08081c.488db8"
            ],
            []
        ]
    },
    {
        "id": "f08271ff.aab01",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Lê 354-359 (IR)",
        "func": "msg.payload = { input: msg.payload, 'fc': 4, 'unitid': 4, 'address': 353 , 'quantity': 7 }\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 432.7937469482422,
        "y": 1514.158793926239,
        "wires": [
            [
                "e39242de.dcda7"
            ]
        ]
    },
    {
        "id": "3eaace59.89af62",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Lê 1-25 (HR)",
        "func": "msg.payload = { input: msg.payload, 'fc': 3, 'unitid': 4, 'address': 0 , 'quantity': 26 }\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 425.0160140991211,
        "y": 1610.492211341858,
        "wires": [
            [
                "9709c417.9bdce8"
            ]
        ]
    },
    {
        "id": "e39242de.dcda7",
        "type": "modbus-flex-getter",
        "z": "50f61338.29072c",
        "name": "Envia Fila de Leitura GMG4",
        "showStatusActivities": false,
        "showErrors": false,
        "server": "986a090a.461d98",
        "x": 649.7937469482422,
        "y": 1513.158793926239,
        "wires": [
            [
                "2a8c38a2.a3d9b8"
            ],
            []
        ]
    },
    {
        "id": "9709c417.9bdce8",
        "type": "modbus-flex-getter",
        "z": "50f61338.29072c",
        "name": "Envia Fila de Leitura GMG4",
        "showStatusActivities": false,
        "showErrors": false,
        "server": "986a090a.461d98",
        "x": 653.0160064697266,
        "y": 1606.4921660423279,
        "wires": [
            [
                "b5432e87.dd607"
            ],
            []
        ]
    },
    {
        "id": "6bc27d32.23b244",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Lê 132 (IR)",
        "func": "msg.payload = { input: msg.payload, 'fc': 4, 'unitid': 4, 'address': 131 , 'quantity': 1 }\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 417.12705993652344,
        "y": 1560.4921069145203,
        "wires": [
            [
                "37893abd.3501b6"
            ]
        ]
    },
    {
        "id": "37893abd.3501b6",
        "type": "modbus-flex-getter",
        "z": "50f61338.29072c",
        "name": "Envia Fila de Leitura GMG4",
        "showStatusActivities": false,
        "showErrors": false,
        "server": "986a090a.461d98",
        "x": 644.1270599365234,
        "y": 1559.4921069145203,
        "wires": [
            [
                "c545cdda.cc431"
            ],
            []
        ]
    },
    {
        "id": "a52c53c5.b9e5e",
        "type": "modbus-write",
        "z": "50f61338.29072c",
        "name": "Salva GMG4 Local",
        "showStatusActivities": true,
        "showErrors": true,
        "unitid": "1",
        "dataType": "MHoldingRegisters",
        "adr": "165",
        "quantity": "38",
        "server": "a8d40646.cef038",
        "x": 1115.2382049560547,
        "y": 1468.8255968093872,
        "wires": [
            [],
            []
        ]
    },
    {
        "id": "7a9f2ce.e1226d4",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Lê GMG4 local",
        "func": "msg.payload = { input: msg.payload, 'fc': 3, 'unitid': 1, 'address': 165 , 'quantity': 55 }\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 454.2224807739258,
        "y": 1655.397027015686,
        "wires": [
            [
                "6feaf924.6ae938"
            ]
        ]
    },
    {
        "id": "6feaf924.6ae938",
        "type": "modbus-flex-getter",
        "z": "50f61338.29072c",
        "name": "Envia Fila de Leitura GMG4 Local",
        "showStatusActivities": false,
        "showErrors": false,
        "server": "a8d40646.cef038",
        "x": 694.0953330993652,
        "y": 1657.6192164421082,
        "wires": [
            [
                "31f25e19.0ee2a2"
            ],
            []
        ]
    },
    {
        "id": "fd58c2d4.96a3",
        "type": "modbus-write",
        "z": "50f61338.29072c",
        "name": "Salva GMG4 Local",
        "showStatusActivities": true,
        "showErrors": true,
        "unitid": "1",
        "dataType": "MHoldingRegisters",
        "adr": "203",
        "quantity": "4",
        "server": "a8d40646.cef038",
        "x": 1111.151210784912,
        "y": 1513.8891978263855,
        "wires": [
            [],
            []
        ]
    },
    {
        "id": "7b08081c.488db8",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Separa Dados",
        "func": "var todos = {payload: [\nmsg.payload[0], //1   busbar_voltage_12 LSB\nmsg.payload[1], //2   busbar_voltage_12 MSB\nmsg.payload[2], //3   busbar_voltage_23 LSB\nmsg.payload[3], //4   busbar_voltage_23 MSB\nmsg.payload[4], //5   busbar_voltage_31 LSB\nmsg.payload[5], //6   busbar_voltage_31 MSB\nmsg.payload[6], //7   generator_voltage_12 LSB\nmsg.payload[7], //8   generator_voltage_12 MSB\nmsg.payload[8], //9   generator_voltage_23 LSB\nmsg.payload[9], //10  generator_voltage_23 MSB\nmsg.payload[10], //11 generator_voltage_31 LSB\nmsg.payload[11], //12 generator_voltage_31 MSB\n\nmsg.payload[20], //13 current_1 LSB\nmsg.payload[21], //14 current_1 MSB\nmsg.payload[22], //15 current_2 LSB\nmsg.payload[23], //16 current_2 MSB\nmsg.payload[24], //17 current_3 LSB\nmsg.payload[25], //18 current_3 MSB\n\nmsg.payload[28], //19 generator_frequency\nmsg.payload[29], //20 busbar_frequency\n\nmsg.payload[60], //21 current_active_power_total LSB\nmsg.payload[61], //22 current_active_power_total MSB\nmsg.payload[62], //23 current_reactive_power_total LSB\nmsg.payload[63], //24 current_reactive_power_total MSB\nmsg.payload[64], //25 current_apparent_power_total LSB\nmsg.payload[65], //26 current_apparent_power_total MSB\n\nmsg.payload[67], //27 current_pf_total\n\nmsg.payload[70], //28 engine_running_hours LSB\nmsg.payload[71], //29 engine_running_hours MSB\n\nmsg.payload[73], //30 engine_battery_voltage\n\nmsg.payload[76], //31 engine_oil_pressure\n\nmsg.payload[77], //32 engine_coolant_temperature LSB\nmsg.payload[78], //33 engine_coolant_temperature MSB\n\nmsg.payload[80], //34 engine_velocity\n\nmsg.payload[85], //35 generator_active_energy LSB\nmsg.payload[86], //36 generator_active_energy MSB\n\nmsg.payload[93], //37 io_cont_voltage_an_input1_JW\nmsg.payload[94]  //38 io_cont_voltage_an_input2_JW\n]};\n\nreturn todos;",
        "outputs": "1",
        "noerr": 0,
        "x": 876.7382354736328,
        "y": 1468.1034417152405,
        "wires": [
            [
                "a52c53c5.b9e5e"
            ]
        ]
    },
    {
        "id": "2a8c38a2.a3d9b8",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Separa Dados",
        "func": "var todos = {payload: [\nmsg.payload[0], //1 - 354 engine_intake_manifold1_press\n//msg.payload[1], //2 - 355\nmsg.payload[2], //3 - 356 engine_throttle_pos\n//msg.payload[3], //4 - 357\n//msg.payload[4], //5 - 358\nmsg.payload[5], //6 - 359 engine_intake_manifold1_temp LSB\nmsg.payload[6], //7 - 360 engine_intake_manifold1_temp MSB\n]};\n\n\nreturn todos;",
        "outputs": "1",
        "noerr": 0,
        "x": 881.4604949951172,
        "y": 1514.492266178131,
        "wires": [
            [
                "fd58c2d4.96a3"
            ]
        ]
    },
    {
        "id": "c545cdda.cc431",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Separa Dados",
        "func": "var todos = {payload: [\nmsg.payload[0], //1 - 132\n]};\n\nreturn todos;",
        "outputs": "1",
        "noerr": 0,
        "x": 886.460521697998,
        "y": 1555.9923090934753,
        "wires": [
            [
                "38e8314e.45274e"
            ]
        ]
    },
    {
        "id": "38e8314e.45274e",
        "type": "modbus-write",
        "z": "50f61338.29072c",
        "name": "Salva GMG4 Local",
        "showStatusActivities": true,
        "showErrors": true,
        "unitid": "1",
        "dataType": "MHoldingRegisters",
        "adr": "207",
        "quantity": "1",
        "server": "a8d40646.cef038",
        "x": 1108.4608993530273,
        "y": 1556.9923458695412,
        "wires": [
            [],
            []
        ]
    },
    {
        "id": "b5432e87.dd607",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Separa Dados",
        "func": "var todos = {payload: [\nmsg.payload[0], //1   seconds\nmsg.payload[1], //2   minutes\nmsg.payload[2], //3   hours\nmsg.payload[3], //4   day_of_month\n//msg.payload[4], //5 \nmsg.payload[5], //6   month\nmsg.payload[6], //7   year\n//msg.payload[7], //8 \nmsg.payload[8], //9   engine_running_hours LSB\nmsg.payload[9], //10  engine_running_hours MSB\nmsg.payload[10], //11 number_of_cranks LSB\nmsg.payload[11], //12 number_of_cranks MSB\n//0 a 11 foi\nmsg.payload[24], //13 working_hours_with_load LSB\nmsg.payload[25], //14 working_hours_with_load MSB\n]};\n\n//msg.payload = todos.join();\n//msg.topic=1;\n\nreturn todos;",
        "outputs": "1",
        "noerr": 0,
        "x": 891.4605293273926,
        "y": 1602.492311000824,
        "wires": [
            [
                "ec9ce4e6.b46648"
            ]
        ]
    },
    {
        "id": "ec9ce4e6.b46648",
        "type": "modbus-write",
        "z": "50f61338.29072c",
        "name": "Salva GMG4 Local",
        "showStatusActivities": true,
        "showErrors": true,
        "unitid": "1",
        "dataType": "MHoldingRegisters",
        "adr": "208",
        "quantity": "12",
        "server": "a8d40646.cef038",
        "x": 1112.5082893371582,
        "y": 1598.2542033195496,
        "wires": [
            [],
            []
        ]
    },
    {
        "id": "31f25e19.0ee2a2",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Adequa Dados e Razão",
        "func": "var quatro = 4;\nvar busbar_voltage_12 =  ((msg.payload[1]*65536+msg.payload[0])/256);\nvar busbar_voltage_23 =  ((msg.payload[3]*65536+msg.payload[2])/256);\nvar busbar_voltage_31 =  ((msg.payload[5]*65536+msg.payload[4])/256);\nvar generator_voltage_12 =  ((msg.payload[7]*65536+msg.payload[6])/256);\nvar generator_voltage_23 =  ((msg.payload[9]*65536+msg.payload[8])/256);\nvar generator_voltage_31 =  ((msg.payload[11]*65536+msg.payload[10])/256);\nvar current_1 = ((msg.payload[13]*65536+msg.payload[12])/256);\nvar current_2 =  ((msg.payload[15]*65536+msg.payload[14])/256);\nvar current_3 =  ((msg.payload[17]*65536+msg.payload[16])/256);\nvar generator_frequency =  (msg.payload[18]/256);\nvar busbar_frequency =  (msg.payload[19]/256);\n\nvar current_active_power_total =  ((msg.payload[21]*65536+msg.payload[20])/256);\nif(current_active_power_total>8388607){current_active_power_total=current_active_power_total-16777215;}\n\nvar current_reactive_power_total =  ((msg.payload[23]*65536+msg.payload[22])/256);\nif(current_reactive_power_total>8388607){current_reactive_power_total=current_reactive_power_total-16777215;}\n\nvar current_apparent_power_total =  ((msg.payload[25]*65536+msg.payload[24])/256);\n\nvar current_pf_total =  (msg.payload[26]/256);\nif(current_pf_total>8388607){current_pf_total=current_pf_total-16777215;}\n\n//var engine_running_hours =  ((msg.payload[28]*65536+msg.payload[27]));\nvar engine_battery_voltage =  (msg.payload[29]/256);\nvar engine_oil_pressure =  (msg.payload[30]/256);\nvar engine_coolant_temperature =  ((msg.payload[32]*65536+msg.payload[31])/256);\nvar engine_velocity =  (msg.payload[33]);\nvar generator_active_energy =  ((msg.payload[35]*65536+msg.payload[34]));\nvar io_cont_voltage_an_input1_JW =  (msg.payload[36]/256);\nvar io_cont_voltage_an_input2_JW =  (msg.payload[37]/256);\n//ok 0 a 37 = 38\n\nvar engine_intake_manifold1_press =  (msg.payload[38]*1/256 ); //354\nvar engine_throttle_pos =  (msg.payload[39]*1/256 ); //356\nvar engine_intake_manifold1_temp =  ((msg.payload[41]*65536+msg.payload[40])*1/256 ); //359\n//ok 4\n\nvar engine_status = ((msg.payload[42])); \n//ok 1\n\nvar seconds = ((msg.payload[43])); //1\nvar minutes =  ((msg.payload[44])); //2\nvar hours =  ((msg.payload[45])); //3\nvar day_of_month =  ((msg.payload[46])); //4\nvar month =  ((msg.payload[47]));//5\nvar year =  ((msg.payload[48]));//6\nvar engine_working_hours =  ((msg.payload[50]*65536+msg.payload[49]) );//7-8\nvar number_of_cranks = ((msg.payload[52]*65536+msg.payload[51]) );//9-10\nvar engine_working_hours_with_load = ((msg.payload[54]*65536+msg.payload[53]) );//11-12\n\nvar todos = {payload: [\nquatro,\nbusbar_voltage_12,\nbusbar_voltage_23,\nbusbar_voltage_31,\ngenerator_voltage_12,\ngenerator_voltage_23,\ngenerator_voltage_31,\ncurrent_1,\ncurrent_2,\ncurrent_3,\ngenerator_frequency,\nbusbar_frequency,\ncurrent_active_power_total,\ncurrent_reactive_power_total,\ncurrent_apparent_power_total,\ncurrent_pf_total,\nengine_battery_voltage,\nengine_oil_pressure,\nengine_coolant_temperature,\nengine_velocity,\ngenerator_active_energy,\nio_cont_voltage_an_input1_JW,\nio_cont_voltage_an_input2_JW,\n\nengine_intake_manifold1_press,\nengine_throttle_pos,\nengine_intake_manifold1_temp,\n\nengine_status,\n\nseconds,\nminutes,\nhours,\nday_of_month,\nmonth,\nyear,\nengine_working_hours,\nnumber_of_cranks,\nengine_working_hours_with_load\n]};\n\n\n\nreturn todos;//msg;\n",
        "outputs": "1",
        "noerr": 0,
        "x": 967.8414688110352,
        "y": 1658.9210119247437,
        "wires": [
            [
                "d2ec9279.62d9a"
            ]
        ]
    },
    {
        "id": "d2ec9279.62d9a",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "INSERIR NO BANCO DE DADOS",
        "func": "msg.topic =\"SET time_zone='America/Sao_Paulo'; INSERT INTO `dados_brasilgtw`.`dados` (`id_dispositivo`,`busbar_voltage_12`,`busbar_voltage_23`,`busbar_voltage_31`,`generator_voltage_12`,`generator_voltage_23`,`generator_voltage_31`,`current_1`,`current_2`,`current_3`,`generator_frequency`,`busbar_frequency`,`current_active_power_total`,`current_reactive_power_total`,`current_apparent_power_total`,`current_pf_total`,`engine_battery_voltage`,`engine_oil_pressure`,`engine_coolant_temperature`,`engine_velocity`,`generator_active_energy`,`io_cont_voltage_an_input1_JW`,`io_cont_voltage_an_input2_JW`,`engine_intake_manifold1_press`,`engine_throttle_pos`,`engine_intake_manifold1_temp`,`engine_status`,`seconds`,`minutes`,`hours`,`day_of_month`,`month`,`year`,`engine_working_hours`,`number_of_cranks`,`engine_working_hours_with_load`) VALUES (\"+msg.payload+\")\";\n\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 1255.5558853149414,
        "y": 1652.7937698364258,
        "wires": [
            [
                "2a03d611.26c39a"
            ]
        ]
    },
    {
        "id": "4ec32a22.dc9bd4",
        "type": "delay",
        "z": "50f61338.29072c",
        "name": "",
        "pauseType": "delay",
        "timeout": "1",
        "timeoutUnits": "milliseconds",
        "rate": "1",
        "nbRateUnits": "1",
        "rateUnits": "second",
        "randomFirst": "1",
        "randomLast": "5",
        "randomUnits": "seconds",
        "drop": false,
        "x": 136.68260955810547,
        "y": 1487.2699556350708,
        "wires": [
            [
                "abd8f923.456568",
                "f08271ff.aab01",
                "6bc27d32.23b244",
                "3eaace59.89af62",
                "7a9f2ce.e1226d4"
            ]
        ]
    },
    {
        "id": "d732f999.c69898",
        "type": "catch",
        "z": "50f61338.29072c",
        "name": "",
        "scope": null,
        "x": 425.2221488952637,
        "y": 1784.9998779296875,
        "wires": [
            [
                "58d7e9ab.7d1b28"
            ]
        ]
    },
    {
        "id": "2582717.ad8418e",
        "type": "modbus-queue-info",
        "z": "50f61338.29072c",
        "name": "Fila Leitura GMG5 Remoto",
        "unitid": "5",
        "lowLowLevel": 25,
        "lowLevel": 75,
        "highLevel": 150,
        "highHighLevel": 300,
        "server": "986a090a.461d98",
        "errorOnHighLevel": false,
        "x": 1002.444450378418,
        "y": 1778.7777032852173,
        "wires": [
            [
                "d3e384e9.40c458"
            ]
        ]
    },
    {
        "id": "58d7e9ab.7d1b28",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Reseta leitura se atingir nivel high high",
        "func": "if(\"high high level reached\" === msg.state && \n    msg.unitid === 5 &&\n    msg.error.source.name === \"Read Queue\") {\n    msg.resetQueue = true;\n    return msg;\n}\n",
        "outputs": 1,
        "noerr": 0,
        "x": 685.5555191040039,
        "y": 1783.2221193313599,
        "wires": [
            [
                "2582717.ad8418e"
            ]
        ]
    },
    {
        "id": "d3e384e9.40c458",
        "type": "debug",
        "z": "50f61338.29072c",
        "name": "",
        "active": false,
        "console": "false",
        "complete": "payload",
        "x": 1239.2541913986206,
        "y": 1779.555452823639,
        "wires": []
    },
    {
        "id": "68eb125d.e4e23c",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Lê 1 a 95 (IR)",
        "func": "msg.payload = { input: msg.payload, 'fc': 4, 'unitid': 5, 'address': 0 , 'quantity': 94 }\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 440.4444885253906,
        "y": 1836.761890411377,
        "wires": [
            [
                "af041e32.b520d"
            ]
        ]
    },
    {
        "id": "af041e32.b520d",
        "type": "modbus-flex-getter",
        "z": "50f61338.29072c",
        "name": "Envia Fila de Leitura GMG5",
        "showStatusActivities": false,
        "showErrors": false,
        "server": "986a090a.461d98",
        "x": 659.0000839233398,
        "y": 1842.7618608474731,
        "wires": [
            [
                "3ea3274e.4b1ea8"
            ],
            []
        ]
    },
    {
        "id": "c91548ff.078b68",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Lê 354-359 (IR)",
        "func": "msg.payload = { input: msg.payload, 'fc': 4, 'unitid': 5, 'address': 353 , 'quantity': 7 }\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 444.44446563720703,
        "y": 1885.7618398666382,
        "wires": [
            [
                "7bc898db.8fd528"
            ]
        ]
    },
    {
        "id": "d6f33d7a.fa30d",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Lê 1-25 (HR)",
        "func": "msg.payload = { input: msg.payload, 'fc': 3, 'unitid': 5, 'address': 0 , 'quantity': 26 }\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 436.66673278808594,
        "y": 1982.095257282257,
        "wires": [
            [
                "17aa0f17.9e8b41"
            ]
        ]
    },
    {
        "id": "7bc898db.8fd528",
        "type": "modbus-flex-getter",
        "z": "50f61338.29072c",
        "name": "Envia Fila de Leitura GMG5",
        "showStatusActivities": false,
        "showErrors": false,
        "server": "986a090a.461d98",
        "x": 661.444465637207,
        "y": 1884.7618398666382,
        "wires": [
            [
                "adb79d4d.4d734"
            ],
            []
        ]
    },
    {
        "id": "17aa0f17.9e8b41",
        "type": "modbus-flex-getter",
        "z": "50f61338.29072c",
        "name": "Envia Fila de Leitura GMG5",
        "showStatusActivities": false,
        "showErrors": false,
        "server": "986a090a.461d98",
        "x": 664.6667251586914,
        "y": 1978.095211982727,
        "wires": [
            [
                "95e5cdff.1ff9c"
            ],
            []
        ]
    },
    {
        "id": "e5f02e84.55fd8",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Lê 132 (IR)",
        "func": "msg.payload = { input: msg.payload, 'fc': 4, 'unitid': 5, 'address': 131 , 'quantity': 1 }\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 428.7777786254883,
        "y": 1932.0951528549194,
        "wires": [
            [
                "1b59bf5d.b54b51"
            ]
        ]
    },
    {
        "id": "1b59bf5d.b54b51",
        "type": "modbus-flex-getter",
        "z": "50f61338.29072c",
        "name": "Envia Fila de Leitura GMG5",
        "showStatusActivities": false,
        "showErrors": false,
        "server": "986a090a.461d98",
        "x": 655.7777786254883,
        "y": 1931.0951528549194,
        "wires": [
            [
                "ee7b7eac.f90a8"
            ],
            []
        ]
    },
    {
        "id": "4fbc15ba.e5312c",
        "type": "modbus-write",
        "z": "50f61338.29072c",
        "name": "Salva GMG5 Local",
        "showStatusActivities": true,
        "showErrors": true,
        "unitid": "1",
        "dataType": "MHoldingRegisters",
        "adr": "220",
        "quantity": "38",
        "server": "a8d40646.cef038",
        "x": 1126.8889236450195,
        "y": 1840.4286427497864,
        "wires": [
            [],
            []
        ]
    },
    {
        "id": "625250bf.410c",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Lê GMG5 local",
        "func": "msg.payload = { input: msg.payload, 'fc': 3, 'unitid': 1, 'address': 220 , 'quantity': 55 }\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 465.8731994628906,
        "y": 2027.0000729560852,
        "wires": [
            [
                "ac0cc8d2.22b318"
            ]
        ]
    },
    {
        "id": "ac0cc8d2.22b318",
        "type": "modbus-flex-getter",
        "z": "50f61338.29072c",
        "name": "Envia Fila de Leitura GMG5 Local",
        "showStatusActivities": false,
        "showErrors": false,
        "server": "a8d40646.cef038",
        "x": 705.7460517883301,
        "y": 2029.2222623825073,
        "wires": [
            [
                "e0ad0596.9e2e88"
            ],
            []
        ]
    },
    {
        "id": "3df261a0.a954fe",
        "type": "modbus-write",
        "z": "50f61338.29072c",
        "name": "Salva GMG5 Local",
        "showStatusActivities": true,
        "showErrors": true,
        "unitid": "1",
        "dataType": "MHoldingRegisters",
        "adr": "258",
        "quantity": "4",
        "server": "a8d40646.cef038",
        "x": 1122.801929473877,
        "y": 1885.4922437667847,
        "wires": [
            [],
            []
        ]
    },
    {
        "id": "3ea3274e.4b1ea8",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Separa Dados",
        "func": "var todos = {payload: [\nmsg.payload[0], //1   busbar_voltage_12 LSB\nmsg.payload[1], //2   busbar_voltage_12 MSB\nmsg.payload[2], //3   busbar_voltage_23 LSB\nmsg.payload[3], //4   busbar_voltage_23 MSB\nmsg.payload[4], //5   busbar_voltage_31 LSB\nmsg.payload[5], //6   busbar_voltage_31 MSB\nmsg.payload[6], //7   generator_voltage_12 LSB\nmsg.payload[7], //8   generator_voltage_12 MSB\nmsg.payload[8], //9   generator_voltage_23 LSB\nmsg.payload[9], //10  generator_voltage_23 MSB\nmsg.payload[10], //11 generator_voltage_31 LSB\nmsg.payload[11], //12 generator_voltage_31 MSB\n\nmsg.payload[20], //13 current_1 LSB\nmsg.payload[21], //14 current_1 MSB\nmsg.payload[22], //15 current_2 LSB\nmsg.payload[23], //16 current_2 MSB\nmsg.payload[24], //17 current_3 LSB\nmsg.payload[25], //18 current_3 MSB\n\nmsg.payload[28], //19 generator_frequency\nmsg.payload[29], //20 busbar_frequency\n\nmsg.payload[60], //21 current_active_power_total LSB\nmsg.payload[61], //22 current_active_power_total MSB\nmsg.payload[62], //23 current_reactive_power_total LSB\nmsg.payload[63], //24 current_reactive_power_total MSB\nmsg.payload[64], //25 current_apparent_power_total LSB\nmsg.payload[65], //26 current_apparent_power_total MSB\n\nmsg.payload[67], //27 current_pf_total\n\nmsg.payload[70], //28 engine_running_hours LSB\nmsg.payload[71], //29 engine_running_hours MSB\n\nmsg.payload[73], //30 engine_battery_voltage\n\nmsg.payload[76], //31 engine_oil_pressure\n\nmsg.payload[77], //32 engine_coolant_temperature LSB\nmsg.payload[78], //33 engine_coolant_temperature MSB\n\nmsg.payload[80], //34 engine_velocity\n\nmsg.payload[85], //35 generator_active_energy LSB\nmsg.payload[86], //36 generator_active_energy MSB\n\nmsg.payload[93], //37 io_cont_voltage_an_input1_JW\nmsg.payload[94]  //38 io_cont_voltage_an_input2_JW\n]};\n\nreturn todos;",
        "outputs": "1",
        "noerr": 0,
        "x": 888.3889541625977,
        "y": 1839.7064876556396,
        "wires": [
            [
                "4fbc15ba.e5312c"
            ]
        ]
    },
    {
        "id": "adb79d4d.4d734",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Separa Dados",
        "func": "var todos = {payload: [\nmsg.payload[0], //1 - 354 engine_intake_manifold1_press\n//msg.payload[1], //2 - 355\nmsg.payload[2], //3 - 356 engine_throttle_pos\n//msg.payload[3], //4 - 357\n//msg.payload[4], //5 - 358\nmsg.payload[5], //6 - 359 engine_intake_manifold1_temp LSB\nmsg.payload[6], //7 - 360 engine_intake_manifold1_temp MSB\n]};\n\n\nreturn todos;",
        "outputs": "1",
        "noerr": 0,
        "x": 893.111213684082,
        "y": 1886.0953121185303,
        "wires": [
            [
                "3df261a0.a954fe"
            ]
        ]
    },
    {
        "id": "ee7b7eac.f90a8",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Separa Dados",
        "func": "var todos = {payload: [\nmsg.payload[0], //1 - 132\n]};\n\nreturn todos;",
        "outputs": "1",
        "noerr": 0,
        "x": 898.1112403869629,
        "y": 1927.5953550338745,
        "wires": [
            [
                "7f5a8121.fbd13"
            ]
        ]
    },
    {
        "id": "7f5a8121.fbd13",
        "type": "modbus-write",
        "z": "50f61338.29072c",
        "name": "Salva GMG5 Local",
        "showStatusActivities": true,
        "showErrors": true,
        "unitid": "1",
        "dataType": "MHoldingRegisters",
        "adr": "262",
        "quantity": "1",
        "server": "a8d40646.cef038",
        "x": 1120.1116180419922,
        "y": 1928.5953918099403,
        "wires": [
            [],
            []
        ]
    },
    {
        "id": "95e5cdff.1ff9c",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Separa Dados",
        "func": "var todos = {payload: [\nmsg.payload[0], //1   seconds\nmsg.payload[1], //2   minutes\nmsg.payload[2], //3   hours\nmsg.payload[3], //4   day_of_month\n//msg.payload[4], //5 \nmsg.payload[5], //6   month\nmsg.payload[6], //7   year\n//msg.payload[7], //8 \nmsg.payload[8], //9   engine_running_hours LSB\nmsg.payload[9], //10  engine_running_hours MSB\nmsg.payload[10], //11 number_of_cranks LSB\nmsg.payload[11], //12 number_of_cranks MSB\n//0 a 11 foi\nmsg.payload[24], //13 working_hours_with_load LSB\nmsg.payload[25], //14 working_hours_with_load MSB\n]};\n\n//msg.payload = todos.join();\n//msg.topic=1;\n\nreturn todos;",
        "outputs": "1",
        "noerr": 0,
        "x": 903.1112480163574,
        "y": 1974.0953569412231,
        "wires": [
            [
                "2a42b22e.a414ae"
            ]
        ]
    },
    {
        "id": "2a42b22e.a414ae",
        "type": "modbus-write",
        "z": "50f61338.29072c",
        "name": "Salva GMG5 Local",
        "showStatusActivities": true,
        "showErrors": true,
        "unitid": "1",
        "dataType": "MHoldingRegisters",
        "adr": "263",
        "quantity": "12",
        "server": "a8d40646.cef038",
        "x": 1124.159008026123,
        "y": 1969.8572492599487,
        "wires": [
            [],
            []
        ]
    },
    {
        "id": "e0ad0596.9e2e88",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Adequa Dados e Razão",
        "func": "var cinco = 5;\nvar busbar_voltage_12 =  ((msg.payload[1]*65536+msg.payload[0])/256);\nvar busbar_voltage_23 =  ((msg.payload[3]*65536+msg.payload[2])/256);\nvar busbar_voltage_31 =  ((msg.payload[5]*65536+msg.payload[4])/256);\nvar generator_voltage_12 =  ((msg.payload[7]*65536+msg.payload[6])/256);\nvar generator_voltage_23 =  ((msg.payload[9]*65536+msg.payload[8])/256);\nvar generator_voltage_31 =  ((msg.payload[11]*65536+msg.payload[10])/256);\nvar current_1 = ((msg.payload[13]*65536+msg.payload[12])/256);\nvar current_2 =  ((msg.payload[15]*65536+msg.payload[14])/256);\nvar current_3 =  ((msg.payload[17]*65536+msg.payload[16])/256);\nvar generator_frequency =  (msg.payload[18]/256);\nvar busbar_frequency =  (msg.payload[19]/256);\n\nvar current_active_power_total =  ((msg.payload[21]*65536+msg.payload[20])/256);\nif(current_active_power_total>8388607){current_active_power_total=current_active_power_total-16777215;}\n\nvar current_reactive_power_total =  ((msg.payload[23]*65536+msg.payload[22])/256);\nif(current_reactive_power_total>8388607){current_reactive_power_total=current_reactive_power_total-16777215;}\n\nvar current_apparent_power_total =  ((msg.payload[25]*65536+msg.payload[24])/256);\n\nvar current_pf_total =  (msg.payload[26]/256);\nif(current_pf_total>8388607){current_pf_total=current_pf_total-16777215;}\n\n//var engine_running_hours =  ((msg.payload[28]*65536+msg.payload[27]));\nvar engine_battery_voltage =  (msg.payload[29]/256);\nvar engine_oil_pressure =  (msg.payload[30]/256);\nvar engine_coolant_temperature =  ((msg.payload[32]*65536+msg.payload[31])/256);\nvar engine_velocity =  (msg.payload[33]);\nvar generator_active_energy =  ((msg.payload[35]*65536+msg.payload[34]));\nvar io_cont_voltage_an_input1_JW =  (msg.payload[36]/256);\nvar io_cont_voltage_an_input2_JW =  (msg.payload[37]/256);\n//ok 0 a 37 = 38\n\nvar engine_intake_manifold1_press =  (msg.payload[38]*1/256 ); //354\nvar engine_throttle_pos =  (msg.payload[39]*1/256 ); //356\nvar engine_intake_manifold1_temp =  ((msg.payload[41]*65536+msg.payload[40])*1/256 ); //359\n//ok 4\n\nvar engine_status = ((msg.payload[42])); \n//ok 1\n\nvar seconds = ((msg.payload[43])); //1\nvar minutes =  ((msg.payload[44])); //2\nvar hours =  ((msg.payload[45])); //3\nvar day_of_month =  ((msg.payload[46])); //4\nvar month =  ((msg.payload[47]));//5\nvar year =  ((msg.payload[48]));//6\nvar engine_working_hours =  ((msg.payload[50]*65536+msg.payload[49]) );//7-8\nvar number_of_cranks = ((msg.payload[52]*65536+msg.payload[51]) );//9-10\nvar engine_working_hours_with_load = ((msg.payload[54]*65536+msg.payload[53]) );//11-12\n\nvar todos = {payload: [\ncinco,\nbusbar_voltage_12,\nbusbar_voltage_23,\nbusbar_voltage_31,\ngenerator_voltage_12,\ngenerator_voltage_23,\ngenerator_voltage_31,\ncurrent_1,\ncurrent_2,\ncurrent_3,\ngenerator_frequency,\nbusbar_frequency,\ncurrent_active_power_total,\ncurrent_reactive_power_total,\ncurrent_apparent_power_total,\ncurrent_pf_total,\nengine_battery_voltage,\nengine_oil_pressure,\nengine_coolant_temperature,\nengine_velocity,\ngenerator_active_energy,\nio_cont_voltage_an_input1_JW,\nio_cont_voltage_an_input2_JW,\n\nengine_intake_manifold1_press,\nengine_throttle_pos,\nengine_intake_manifold1_temp,\n\nengine_status,\n\nseconds,\nminutes,\nhours,\nday_of_month,\nmonth,\nyear,\nengine_working_hours,\nnumber_of_cranks,\nengine_working_hours_with_load\n]};\n\n\n\nreturn todos;//msg;\n",
        "outputs": "1",
        "noerr": 0,
        "x": 979.4921875,
        "y": 2030.5240578651428,
        "wires": [
            [
                "e17fa42c.76cc78"
            ]
        ]
    },
    {
        "id": "e17fa42c.76cc78",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "INSERIR NO BANCO DE DADOS",
        "func": "msg.topic =\"SET time_zone='America/Sao_Paulo'; INSERT INTO `dados_brasilgtw`.`dados` (`id_dispositivo`,`busbar_voltage_12`,`busbar_voltage_23`,`busbar_voltage_31`,`generator_voltage_12`,`generator_voltage_23`,`generator_voltage_31`,`current_1`,`current_2`,`current_3`,`generator_frequency`,`busbar_frequency`,`current_active_power_total`,`current_reactive_power_total`,`current_apparent_power_total`,`current_pf_total`,`engine_battery_voltage`,`engine_oil_pressure`,`engine_coolant_temperature`,`engine_velocity`,`generator_active_energy`,`io_cont_voltage_an_input1_JW`,`io_cont_voltage_an_input2_JW`,`engine_intake_manifold1_press`,`engine_throttle_pos`,`engine_intake_manifold1_temp`,`engine_status`,`seconds`,`minutes`,`hours`,`day_of_month`,`month`,`year`,`engine_working_hours`,`number_of_cranks`,`engine_working_hours_with_load`) VALUES (\"+msg.payload+\")\";\n\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 1267.2066040039062,
        "y": 2024.396815776825,
        "wires": [
            [
                "2a03d611.26c39a"
            ]
        ]
    },
    {
        "id": "76e80312.229e8c",
        "type": "delay",
        "z": "50f61338.29072c",
        "name": "",
        "pauseType": "delay",
        "timeout": "1",
        "timeoutUnits": "milliseconds",
        "rate": "1",
        "nbRateUnits": "1",
        "rateUnits": "second",
        "randomFirst": "1",
        "randomLast": "5",
        "randomUnits": "seconds",
        "drop": false,
        "x": 148.3333282470703,
        "y": 1858.87300157547,
        "wires": [
            [
                "68eb125d.e4e23c",
                "c91548ff.078b68",
                "e5f02e84.55fd8",
                "d6f33d7a.fa30d",
                "625250bf.410c"
            ]
        ]
    },
    {
        "id": "414de869.54d2c8",
        "type": "catch",
        "z": "50f61338.29072c",
        "name": "",
        "scope": null,
        "x": 451.88882064819336,
        "y": 2138.333251953125,
        "wires": [
            [
                "83f3a6.68b70c58"
            ]
        ]
    },
    {
        "id": "ede7bf9d.34767",
        "type": "modbus-queue-info",
        "z": "50f61338.29072c",
        "name": "Fila Leitura GMG6 Remoto",
        "unitid": "6",
        "lowLowLevel": 25,
        "lowLevel": 75,
        "highLevel": 150,
        "highHighLevel": 300,
        "server": "986a090a.461d98",
        "errorOnHighLevel": false,
        "x": 1029.1111221313477,
        "y": 2132.111077308655,
        "wires": [
            [
                "cd0d407b.b2cbf"
            ]
        ]
    },
    {
        "id": "83f3a6.68b70c58",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Reseta leitura se atingir nivel high high",
        "func": "if(\"high high level reached\" === msg.state && \n    msg.unitid === 6 &&\n    msg.error.source.name === \"Read Queue\") {\n    msg.resetQueue = true;\n    return msg;\n}\n",
        "outputs": 1,
        "noerr": 0,
        "x": 712.2221908569336,
        "y": 2136.5554933547974,
        "wires": [
            [
                "ede7bf9d.34767"
            ]
        ]
    },
    {
        "id": "cd0d407b.b2cbf",
        "type": "debug",
        "z": "50f61338.29072c",
        "name": "",
        "active": false,
        "console": "false",
        "complete": "payload",
        "x": 1265.9208631515503,
        "y": 2132.8888268470764,
        "wires": []
    },
    {
        "id": "499000f8.b1933",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Lê 1 a 95 (IR)",
        "func": "msg.payload = { input: msg.payload, 'fc': 4, 'unitid': 6, 'address': 0 , 'quantity': 94 }\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 467.1111602783203,
        "y": 2190.0952644348145,
        "wires": [
            [
                "84d1dff3.a892e"
            ]
        ]
    },
    {
        "id": "84d1dff3.a892e",
        "type": "modbus-flex-getter",
        "z": "50f61338.29072c",
        "name": "Envia Fila de Leitura GMG6",
        "showStatusActivities": false,
        "showErrors": false,
        "server": "986a090a.461d98",
        "x": 685.6667556762695,
        "y": 2196.0952348709106,
        "wires": [
            [
                "68863ef.581a4c"
            ],
            []
        ]
    },
    {
        "id": "7baccf89.9722d",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Lê 354-359 (IR)",
        "func": "msg.payload = { input: msg.payload, 'fc': 4, 'unitid': 6, 'address': 353 , 'quantity': 7 }\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 471.1111373901367,
        "y": 2239.0952138900757,
        "wires": [
            [
                "f3c52907.a86948"
            ]
        ]
    },
    {
        "id": "ac7824f9.27a4c8",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Lê 1-25 (HR)",
        "func": "msg.payload = { input: msg.payload, 'fc': 3, 'unitid': 6, 'address': 0 , 'quantity': 26 }\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 463.3334045410156,
        "y": 2335.4286313056946,
        "wires": [
            [
                "358ad4a1.c4370c"
            ]
        ]
    },
    {
        "id": "f3c52907.a86948",
        "type": "modbus-flex-getter",
        "z": "50f61338.29072c",
        "name": "Envia Fila de Leitura GMG6",
        "showStatusActivities": false,
        "showErrors": false,
        "server": "986a090a.461d98",
        "x": 688.1111373901367,
        "y": 2238.0952138900757,
        "wires": [
            [
                "5b70857d.7bad9c"
            ],
            []
        ]
    },
    {
        "id": "358ad4a1.c4370c",
        "type": "modbus-flex-getter",
        "z": "50f61338.29072c",
        "name": "Envia Fila de Leitura GMG6",
        "showStatusActivities": false,
        "showErrors": false,
        "server": "986a090a.461d98",
        "x": 691.3333969116211,
        "y": 2331.4285860061646,
        "wires": [
            [
                "a5954596.83f908"
            ],
            []
        ]
    },
    {
        "id": "29539e0b.602282",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Lê 132 (IR)",
        "func": "msg.payload = { input: msg.payload, 'fc': 4, 'unitid': 6, 'address': 131 , 'quantity': 1 }\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 455.44445037841797,
        "y": 2285.428526878357,
        "wires": [
            [
                "1de5a862.677ee8"
            ]
        ]
    },
    {
        "id": "1de5a862.677ee8",
        "type": "modbus-flex-getter",
        "z": "50f61338.29072c",
        "name": "Envia Fila de Leitura GMG6",
        "showStatusActivities": false,
        "showErrors": false,
        "server": "986a090a.461d98",
        "x": 682.444450378418,
        "y": 2284.428526878357,
        "wires": [
            [
                "5a204012.699e3"
            ],
            []
        ]
    },
    {
        "id": "78898aef.de3dd4",
        "type": "modbus-write",
        "z": "50f61338.29072c",
        "name": "Salva GMG6 Local",
        "showStatusActivities": true,
        "showErrors": true,
        "unitid": "1",
        "dataType": "MHoldingRegisters",
        "adr": "275",
        "quantity": "38",
        "server": "a8d40646.cef038",
        "x": 1153.5555953979492,
        "y": 2193.762016773224,
        "wires": [
            [],
            []
        ]
    },
    {
        "id": "9b13c77f.350858",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Lê GMG6 local",
        "func": "msg.payload = { input: msg.payload, 'fc': 3, 'unitid': 1, 'address': 275 , 'quantity': 55 }\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 492.5398712158203,
        "y": 2380.3334469795227,
        "wires": [
            [
                "f08827e7.833b18"
            ]
        ]
    },
    {
        "id": "f08827e7.833b18",
        "type": "modbus-flex-getter",
        "z": "50f61338.29072c",
        "name": "Envia Fila de Leitura GMG6 Local",
        "showStatusActivities": false,
        "showErrors": false,
        "server": "a8d40646.cef038",
        "x": 732.4127235412598,
        "y": 2382.555636405945,
        "wires": [
            [
                "6a1c08ef.a8ca58"
            ],
            []
        ]
    },
    {
        "id": "ef7356c6.406cf8",
        "type": "modbus-write",
        "z": "50f61338.29072c",
        "name": "Salva GMG6 Local",
        "showStatusActivities": true,
        "showErrors": true,
        "unitid": "1",
        "dataType": "MHoldingRegisters",
        "adr": "313",
        "quantity": "4",
        "server": "a8d40646.cef038",
        "x": 1149.4686012268066,
        "y": 2238.825617790222,
        "wires": [
            [],
            []
        ]
    },
    {
        "id": "68863ef.581a4c",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Separa Dados",
        "func": "var todos = {payload: [\nmsg.payload[0], //1   busbar_voltage_12 LSB\nmsg.payload[1], //2   busbar_voltage_12 MSB\nmsg.payload[2], //3   busbar_voltage_23 LSB\nmsg.payload[3], //4   busbar_voltage_23 MSB\nmsg.payload[4], //5   busbar_voltage_31 LSB\nmsg.payload[5], //6   busbar_voltage_31 MSB\nmsg.payload[6], //7   generator_voltage_12 LSB\nmsg.payload[7], //8   generator_voltage_12 MSB\nmsg.payload[8], //9   generator_voltage_23 LSB\nmsg.payload[9], //10  generator_voltage_23 MSB\nmsg.payload[10], //11 generator_voltage_31 LSB\nmsg.payload[11], //12 generator_voltage_31 MSB\n\nmsg.payload[20], //13 current_1 LSB\nmsg.payload[21], //14 current_1 MSB\nmsg.payload[22], //15 current_2 LSB\nmsg.payload[23], //16 current_2 MSB\nmsg.payload[24], //17 current_3 LSB\nmsg.payload[25], //18 current_3 MSB\n\nmsg.payload[28], //19 generator_frequency\nmsg.payload[29], //20 busbar_frequency\n\nmsg.payload[60], //21 current_active_power_total LSB\nmsg.payload[61], //22 current_active_power_total MSB\nmsg.payload[62], //23 current_reactive_power_total LSB\nmsg.payload[63], //24 current_reactive_power_total MSB\nmsg.payload[64], //25 current_apparent_power_total LSB\nmsg.payload[65], //26 current_apparent_power_total MSB\n\nmsg.payload[67], //27 current_pf_total\n\nmsg.payload[70], //28 engine_running_hours LSB\nmsg.payload[71], //29 engine_running_hours MSB\n\nmsg.payload[73], //30 engine_battery_voltage\n\nmsg.payload[76], //31 engine_oil_pressure\n\nmsg.payload[77], //32 engine_coolant_temperature LSB\nmsg.payload[78], //33 engine_coolant_temperature MSB\n\nmsg.payload[80], //34 engine_velocity\n\nmsg.payload[85], //35 generator_active_energy LSB\nmsg.payload[86], //36 generator_active_energy MSB\n\nmsg.payload[93], //37 io_cont_voltage_an_input1_JW\nmsg.payload[94]  //38 io_cont_voltage_an_input2_JW\n]};\n\nreturn todos;",
        "outputs": "1",
        "noerr": 0,
        "x": 915.0556259155273,
        "y": 2193.039861679077,
        "wires": [
            [
                "78898aef.de3dd4"
            ]
        ]
    },
    {
        "id": "5b70857d.7bad9c",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Separa Dados",
        "func": "var todos = {payload: [\nmsg.payload[0], //1 - 354 engine_intake_manifold1_press\n//msg.payload[1], //2 - 355\nmsg.payload[2], //3 - 356 engine_throttle_pos\n//msg.payload[3], //4 - 357\n//msg.payload[4], //5 - 358\nmsg.payload[5], //6 - 359 engine_intake_manifold1_temp LSB\nmsg.payload[6], //7 - 360 engine_intake_manifold1_temp MSB\n]};\n\n\nreturn todos;",
        "outputs": "1",
        "noerr": 0,
        "x": 919.7778854370117,
        "y": 2239.428686141968,
        "wires": [
            [
                "ef7356c6.406cf8"
            ]
        ]
    },
    {
        "id": "5a204012.699e3",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Separa Dados",
        "func": "var todos = {payload: [\nmsg.payload[0], //1 - 132\n]};\n\nreturn todos;",
        "outputs": "1",
        "noerr": 0,
        "x": 924.7779121398926,
        "y": 2280.928729057312,
        "wires": [
            [
                "2c6682d9.aa355e"
            ]
        ]
    },
    {
        "id": "2c6682d9.aa355e",
        "type": "modbus-write",
        "z": "50f61338.29072c",
        "name": "Salva GMG6 Local",
        "showStatusActivities": true,
        "showErrors": true,
        "unitid": "1",
        "dataType": "MHoldingRegisters",
        "adr": "317",
        "quantity": "1",
        "server": "a8d40646.cef038",
        "x": 1146.7782897949219,
        "y": 2281.928765833378,
        "wires": [
            [],
            []
        ]
    },
    {
        "id": "a5954596.83f908",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Separa Dados",
        "func": "var todos = {payload: [\nmsg.payload[0], //1   seconds\nmsg.payload[1], //2   minutes\nmsg.payload[2], //3   hours\nmsg.payload[3], //4   day_of_month\n//msg.payload[4], //5 \nmsg.payload[5], //6   month\nmsg.payload[6], //7   year\n//msg.payload[7], //8 \nmsg.payload[8], //9   engine_running_hours LSB\nmsg.payload[9], //10  engine_running_hours MSB\nmsg.payload[10], //11 number_of_cranks LSB\nmsg.payload[11], //12 number_of_cranks MSB\n//0 a 11 foi\nmsg.payload[24], //13 working_hours_with_load LSB\nmsg.payload[25], //14 working_hours_with_load MSB\n]};\n\n//msg.payload = todos.join();\n//msg.topic=1;\n\nreturn todos;",
        "outputs": "1",
        "noerr": 0,
        "x": 929.7779197692871,
        "y": 2327.4287309646606,
        "wires": [
            [
                "9a1ffe37.e582d"
            ]
        ]
    },
    {
        "id": "9a1ffe37.e582d",
        "type": "modbus-write",
        "z": "50f61338.29072c",
        "name": "Salva GMG6 Local",
        "showStatusActivities": true,
        "showErrors": true,
        "unitid": "1",
        "dataType": "MHoldingRegisters",
        "adr": "318",
        "quantity": "12",
        "server": "a8d40646.cef038",
        "x": 1150.8256797790527,
        "y": 2323.1906232833862,
        "wires": [
            [],
            []
        ]
    },
    {
        "id": "6a1c08ef.a8ca58",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Adequa Dados e Razão",
        "func": "var seis = 6;\nvar busbar_voltage_12 =  ((msg.payload[1]*65536+msg.payload[0])/256);\nvar busbar_voltage_23 =  ((msg.payload[3]*65536+msg.payload[2])/256);\nvar busbar_voltage_31 =  ((msg.payload[5]*65536+msg.payload[4])/256);\nvar generator_voltage_12 =  ((msg.payload[7]*65536+msg.payload[6])/256);\nvar generator_voltage_23 =  ((msg.payload[9]*65536+msg.payload[8])/256);\nvar generator_voltage_31 =  ((msg.payload[11]*65536+msg.payload[10])/256);\nvar current_1 = ((msg.payload[13]*65536+msg.payload[12])/256);\nvar current_2 =  ((msg.payload[15]*65536+msg.payload[14])/256);\nvar current_3 =  ((msg.payload[17]*65536+msg.payload[16])/256);\nvar generator_frequency =  (msg.payload[18]/256);\nvar busbar_frequency =  (msg.payload[19]/256);\n\nvar current_active_power_total =  ((msg.payload[21]*65536+msg.payload[20])/256);\nif(current_active_power_total>8388607){current_active_power_total=current_active_power_total-16777215;}\n\nvar current_reactive_power_total =  ((msg.payload[23]*65536+msg.payload[22])/256);\nif(current_reactive_power_total>8388607){current_reactive_power_total=current_reactive_power_total-16777215;}\n\nvar current_apparent_power_total =  ((msg.payload[25]*65536+msg.payload[24])/256);\n\nvar current_pf_total =  (msg.payload[26]/256);\nif(current_pf_total>8388607){current_pf_total=current_pf_total-16777215;}\n\n//var engine_running_hours =  ((msg.payload[28]*65536+msg.payload[27]));\nvar engine_battery_voltage =  (msg.payload[29]/256);\nvar engine_oil_pressure =  (msg.payload[30]/256);\nvar engine_coolant_temperature =  ((msg.payload[32]*65536+msg.payload[31])/256);\nvar engine_velocity =  (msg.payload[33]);\nvar generator_active_energy =  ((msg.payload[35]*65536+msg.payload[34]));\nvar io_cont_voltage_an_input1_JW =  (msg.payload[36]/256);\nvar io_cont_voltage_an_input2_JW =  (msg.payload[37]/256);\n//ok 0 a 37 = 38\n\nvar engine_intake_manifold1_press =  (msg.payload[38]*1/256 ); //354\nvar engine_throttle_pos =  (msg.payload[39]*1/256 ); //356\nvar engine_intake_manifold1_temp =  ((msg.payload[41]*65536+msg.payload[40])*1/256 ); //359\n//ok 4\n\nvar engine_status = ((msg.payload[42])); \n//ok 1\n\nvar seconds = ((msg.payload[43])); //1\nvar minutes =  ((msg.payload[44])); //2\nvar hours =  ((msg.payload[45])); //3\nvar day_of_month =  ((msg.payload[46])); //4\nvar month =  ((msg.payload[47]));//5\nvar year =  ((msg.payload[48]));//6\nvar engine_working_hours =  ((msg.payload[50]*65536+msg.payload[49]) );//7-8\nvar number_of_cranks = ((msg.payload[52]*65536+msg.payload[51]) );//9-10\nvar engine_working_hours_with_load = ((msg.payload[54]*65536+msg.payload[53]) );//11-12\n\nvar todos = {payload: [\nseis,\nbusbar_voltage_12,\nbusbar_voltage_23,\nbusbar_voltage_31,\ngenerator_voltage_12,\ngenerator_voltage_23,\ngenerator_voltage_31,\ncurrent_1,\ncurrent_2,\ncurrent_3,\ngenerator_frequency,\nbusbar_frequency,\ncurrent_active_power_total,\ncurrent_reactive_power_total,\ncurrent_apparent_power_total,\ncurrent_pf_total,\nengine_battery_voltage,\nengine_oil_pressure,\nengine_coolant_temperature,\nengine_velocity,\ngenerator_active_energy,\nio_cont_voltage_an_input1_JW,\nio_cont_voltage_an_input2_JW,\n\nengine_intake_manifold1_press,\nengine_throttle_pos,\nengine_intake_manifold1_temp,\n\nengine_status,\n\nseconds,\nminutes,\nhours,\nday_of_month,\nmonth,\nyear,\nengine_working_hours,\nnumber_of_cranks,\nengine_working_hours_with_load\n]};\n\n\n\nreturn todos;//msg;\n",
        "outputs": "1",
        "noerr": 0,
        "x": 1006.1588592529297,
        "y": 2383.8574318885803,
        "wires": [
            [
                "9260571.4dc27a8"
            ]
        ]
    },
    {
        "id": "9260571.4dc27a8",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "INSERIR NO BANCO DE DADOS",
        "func": "msg.topic =\"SET time_zone='America/Sao_Paulo'; INSERT INTO `dados_brasilgtw`.`dados` (`id_dispositivo`,`busbar_voltage_12`,`busbar_voltage_23`,`busbar_voltage_31`,`generator_voltage_12`,`generator_voltage_23`,`generator_voltage_31`,`current_1`,`current_2`,`current_3`,`generator_frequency`,`busbar_frequency`,`current_active_power_total`,`current_reactive_power_total`,`current_apparent_power_total`,`current_pf_total`,`engine_battery_voltage`,`engine_oil_pressure`,`engine_coolant_temperature`,`engine_velocity`,`generator_active_energy`,`io_cont_voltage_an_input1_JW`,`io_cont_voltage_an_input2_JW`,`engine_intake_manifold1_press`,`engine_throttle_pos`,`engine_intake_manifold1_temp`,`engine_status`,`seconds`,`minutes`,`hours`,`day_of_month`,`month`,`year`,`engine_working_hours`,`number_of_cranks`,`engine_working_hours_with_load`) VALUES (\"+msg.payload+\")\";\n\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 1293.873275756836,
        "y": 2377.7301898002625,
        "wires": [
            [
                "2a03d611.26c39a"
            ]
        ]
    },
    {
        "id": "5dbf667b.69d548",
        "type": "delay",
        "z": "50f61338.29072c",
        "name": "",
        "pauseType": "delay",
        "timeout": "1",
        "timeoutUnits": "milliseconds",
        "rate": "1",
        "nbRateUnits": "1",
        "rateUnits": "second",
        "randomFirst": "1",
        "randomLast": "5",
        "randomUnits": "seconds",
        "drop": false,
        "x": 175,
        "y": 2212.2063755989075,
        "wires": [
            [
                "499000f8.b1933",
                "7baccf89.9722d",
                "29539e0b.602282",
                "ac7824f9.27a4c8",
                "9b13c77f.350858"
            ]
        ]
    },
    {
        "id": "c4c02612.dcaab8",
        "type": "catch",
        "z": "50f61338.29072c",
        "name": "",
        "scope": null,
        "x": 426.66665267944336,
        "y": 2503.333200454712,
        "wires": [
            [
                "c977f421.6b1ca8"
            ]
        ]
    },
    {
        "id": "a0901135.2a3d6",
        "type": "modbus-queue-info",
        "z": "50f61338.29072c",
        "name": "Fila Leitura GMG7 Remoto",
        "unitid": "7",
        "lowLowLevel": 25,
        "lowLevel": 75,
        "highLevel": 150,
        "highHighLevel": 300,
        "server": "986a090a.461d98",
        "errorOnHighLevel": false,
        "x": 1003.8889541625977,
        "y": 2497.1110258102417,
        "wires": [
            [
                "1a7a2de4.53b172"
            ]
        ]
    },
    {
        "id": "c977f421.6b1ca8",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Reseta leitura se atingir nivel high high",
        "func": "if(\"high high level reached\" === msg.state && \n    msg.unitid === 7 &&\n    msg.error.source.name === \"Read Queue\") {\n    msg.resetQueue = true;\n    return msg;\n}\n",
        "outputs": 1,
        "noerr": 0,
        "x": 687.0000228881836,
        "y": 2501.5554418563843,
        "wires": [
            [
                "a0901135.2a3d6"
            ]
        ]
    },
    {
        "id": "1a7a2de4.53b172",
        "type": "debug",
        "z": "50f61338.29072c",
        "name": "",
        "active": false,
        "console": "false",
        "complete": "payload",
        "x": 1240.6986951828003,
        "y": 2497.8887753486633,
        "wires": []
    },
    {
        "id": "547da5fd.5476ec",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Lê 1 a 95 (IR)",
        "func": "msg.payload = { input: msg.payload, 'fc': 4, 'unitid': 7, 'address': 0 , 'quantity': 94 }\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 441.8889923095703,
        "y": 2555.0952129364014,
        "wires": [
            [
                "7f389d99.b573a4"
            ]
        ]
    },
    {
        "id": "7f389d99.b573a4",
        "type": "modbus-flex-getter",
        "z": "50f61338.29072c",
        "name": "Envia Fila de Leitura GMG7",
        "showStatusActivities": false,
        "showErrors": false,
        "server": "986a090a.461d98",
        "x": 660.4445877075195,
        "y": 2561.0951833724976,
        "wires": [
            [
                "aa5436eb.37b788"
            ],
            []
        ]
    },
    {
        "id": "f7f9da5f.0a6458",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Lê 354-359 (IR)",
        "func": "msg.payload = { input: msg.payload, 'fc': 4, 'unitid': 7, 'address': 353 , 'quantity': 7 }\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 445.8889694213867,
        "y": 2604.0951623916626,
        "wires": [
            [
                "bf8f6320.03777"
            ]
        ]
    },
    {
        "id": "c5065a93.3970b8",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Lê 1-25 (HR)",
        "func": "msg.payload = { input: msg.payload, 'fc': 3, 'unitid': 7, 'address': 0 , 'quantity': 26 }\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 438.1112365722656,
        "y": 2700.4285798072815,
        "wires": [
            [
                "bfeb9b6e.cb3418"
            ]
        ]
    },
    {
        "id": "bf8f6320.03777",
        "type": "modbus-flex-getter",
        "z": "50f61338.29072c",
        "name": "Envia Fila de Leitura GMG7",
        "showStatusActivities": false,
        "showErrors": false,
        "server": "986a090a.461d98",
        "x": 662.8889694213867,
        "y": 2603.0951623916626,
        "wires": [
            [
                "b26ad2a4.c80a3"
            ],
            []
        ]
    },
    {
        "id": "bfeb9b6e.cb3418",
        "type": "modbus-flex-getter",
        "z": "50f61338.29072c",
        "name": "Envia Fila de Leitura GMG7",
        "showStatusActivities": false,
        "showErrors": false,
        "server": "986a090a.461d98",
        "x": 666.1112289428711,
        "y": 2696.4285345077515,
        "wires": [
            [
                "3f1841e7.0a683e"
            ],
            []
        ]
    },
    {
        "id": "d8e6404f.64885",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Lê 132 (IR)",
        "func": "msg.payload = { input: msg.payload, 'fc': 4, 'unitid': 7, 'address': 131 , 'quantity': 1 }\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 430.22228240966797,
        "y": 2650.428475379944,
        "wires": [
            [
                "f51dae7.ca1035"
            ]
        ]
    },
    {
        "id": "f51dae7.ca1035",
        "type": "modbus-flex-getter",
        "z": "50f61338.29072c",
        "name": "Envia Fila de Leitura GMG7",
        "showStatusActivities": false,
        "showErrors": false,
        "server": "986a090a.461d98",
        "x": 657.222282409668,
        "y": 2649.428475379944,
        "wires": [
            [
                "d7c6cbad.1033e8"
            ],
            []
        ]
    },
    {
        "id": "b36b5102.9178c",
        "type": "modbus-write",
        "z": "50f61338.29072c",
        "name": "Salva GMG7 Local",
        "showStatusActivities": true,
        "showErrors": true,
        "unitid": "1",
        "dataType": "MHoldingRegisters",
        "adr": "330",
        "quantity": "38",
        "server": "a8d40646.cef038",
        "x": 1128.3334274291992,
        "y": 2558.761965274811,
        "wires": [
            [],
            []
        ]
    },
    {
        "id": "55fd3067.9139c",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Lê GMG7 local",
        "func": "msg.payload = { input: msg.payload, 'fc': 3, 'unitid': 1, 'address': 330 , 'quantity': 55 }\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 467.3177032470703,
        "y": 2745.3333954811096,
        "wires": [
            [
                "19eec0a1.a167cf"
            ]
        ]
    },
    {
        "id": "19eec0a1.a167cf",
        "type": "modbus-flex-getter",
        "z": "50f61338.29072c",
        "name": "Envia Fila de Leitura GMG7 Local",
        "showStatusActivities": false,
        "showErrors": false,
        "server": "a8d40646.cef038",
        "x": 707.1905555725098,
        "y": 2747.5555849075317,
        "wires": [
            [
                "3b98379f.4f8eb8"
            ],
            []
        ]
    },
    {
        "id": "4be36cc8.72bbf4",
        "type": "modbus-write",
        "z": "50f61338.29072c",
        "name": "Salva GMG7 Local",
        "showStatusActivities": true,
        "showErrors": true,
        "unitid": "1",
        "dataType": "MHoldingRegisters",
        "adr": "368",
        "quantity": "4",
        "server": "a8d40646.cef038",
        "x": 1124.2464332580566,
        "y": 2603.825566291809,
        "wires": [
            [],
            []
        ]
    },
    {
        "id": "aa5436eb.37b788",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Separa Dados",
        "func": "var todos = {payload: [\nmsg.payload[0], //1   busbar_voltage_12 LSB\nmsg.payload[1], //2   busbar_voltage_12 MSB\nmsg.payload[2], //3   busbar_voltage_23 LSB\nmsg.payload[3], //4   busbar_voltage_23 MSB\nmsg.payload[4], //5   busbar_voltage_31 LSB\nmsg.payload[5], //6   busbar_voltage_31 MSB\nmsg.payload[6], //7   generator_voltage_12 LSB\nmsg.payload[7], //8   generator_voltage_12 MSB\nmsg.payload[8], //9   generator_voltage_23 LSB\nmsg.payload[9], //10  generator_voltage_23 MSB\nmsg.payload[10], //11 generator_voltage_31 LSB\nmsg.payload[11], //12 generator_voltage_31 MSB\n\nmsg.payload[20], //13 current_1 LSB\nmsg.payload[21], //14 current_1 MSB\nmsg.payload[22], //15 current_2 LSB\nmsg.payload[23], //16 current_2 MSB\nmsg.payload[24], //17 current_3 LSB\nmsg.payload[25], //18 current_3 MSB\n\nmsg.payload[28], //19 generator_frequency\nmsg.payload[29], //20 busbar_frequency\n\nmsg.payload[60], //21 current_active_power_total LSB\nmsg.payload[61], //22 current_active_power_total MSB\nmsg.payload[62], //23 current_reactive_power_total LSB\nmsg.payload[63], //24 current_reactive_power_total MSB\nmsg.payload[64], //25 current_apparent_power_total LSB\nmsg.payload[65], //26 current_apparent_power_total MSB\n\nmsg.payload[67], //27 current_pf_total\n\nmsg.payload[70], //28 engine_running_hours LSB\nmsg.payload[71], //29 engine_running_hours MSB\n\nmsg.payload[73], //30 engine_battery_voltage\n\nmsg.payload[76], //31 engine_oil_pressure\n\nmsg.payload[77], //32 engine_coolant_temperature LSB\nmsg.payload[78], //33 engine_coolant_temperature MSB\n\nmsg.payload[80], //34 engine_velocity\n\nmsg.payload[85], //35 generator_active_energy LSB\nmsg.payload[86], //36 generator_active_energy MSB\n\nmsg.payload[93], //37 io_cont_voltage_an_input1_JW\nmsg.payload[94]  //38 io_cont_voltage_an_input2_JW\n]};\n\nreturn todos;",
        "outputs": "1",
        "noerr": 0,
        "x": 889.8334579467773,
        "y": 2558.039810180664,
        "wires": [
            [
                "b36b5102.9178c"
            ]
        ]
    },
    {
        "id": "b26ad2a4.c80a3",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Separa Dados",
        "func": "var todos = {payload: [\nmsg.payload[0], //1 - 354 engine_intake_manifold1_press\n//msg.payload[1], //2 - 355\nmsg.payload[2], //3 - 356 engine_throttle_pos\n//msg.payload[3], //4 - 357\n//msg.payload[4], //5 - 358\nmsg.payload[5], //6 - 359 engine_intake_manifold1_temp LSB\nmsg.payload[6], //7 - 360 engine_intake_manifold1_temp MSB\n]};\n\n\nreturn todos;",
        "outputs": "1",
        "noerr": 0,
        "x": 894.5557174682617,
        "y": 2604.4286346435547,
        "wires": [
            [
                "4be36cc8.72bbf4"
            ]
        ]
    },
    {
        "id": "d7c6cbad.1033e8",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Separa Dados",
        "func": "var todos = {payload: [\nmsg.payload[0], //1 - 132\n]};\n\nreturn todos;",
        "outputs": "1",
        "noerr": 0,
        "x": 899.5557441711426,
        "y": 2645.928677558899,
        "wires": [
            [
                "5afb02e0.56380c"
            ]
        ]
    },
    {
        "id": "5afb02e0.56380c",
        "type": "modbus-write",
        "z": "50f61338.29072c",
        "name": "Salva GMG7 Local",
        "showStatusActivities": true,
        "showErrors": true,
        "unitid": "1",
        "dataType": "MHoldingRegisters",
        "adr": "372",
        "quantity": "1",
        "server": "a8d40646.cef038",
        "x": 1121.5561218261719,
        "y": 2646.9287143349648,
        "wires": [
            [],
            []
        ]
    },
    {
        "id": "3f1841e7.0a683e",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Separa Dados",
        "func": "var todos = {payload: [\nmsg.payload[0], //1   seconds\nmsg.payload[1], //2   minutes\nmsg.payload[2], //3   hours\nmsg.payload[3], //4   day_of_month\n//msg.payload[4], //5 \nmsg.payload[5], //6   month\nmsg.payload[6], //7   year\n//msg.payload[7], //8 \nmsg.payload[8], //9   engine_running_hours LSB\nmsg.payload[9], //10  engine_running_hours MSB\nmsg.payload[10], //11 number_of_cranks LSB\nmsg.payload[11], //12 number_of_cranks MSB\n//0 a 11 foi\nmsg.payload[24], //13 working_hours_with_load LSB\nmsg.payload[25], //14 working_hours_with_load MSB\n]};\n\n//msg.payload = todos.join();\n//msg.topic=1;\n\nreturn todos;",
        "outputs": "1",
        "noerr": 0,
        "x": 904.5557518005371,
        "y": 2692.4286794662476,
        "wires": [
            [
                "c9b8f1c6.73a01"
            ]
        ]
    },
    {
        "id": "c9b8f1c6.73a01",
        "type": "modbus-write",
        "z": "50f61338.29072c",
        "name": "Salva GMG7 Local",
        "showStatusActivities": true,
        "showErrors": true,
        "unitid": "1",
        "dataType": "MHoldingRegisters",
        "adr": "373",
        "quantity": "12",
        "server": "a8d40646.cef038",
        "x": 1125.6035118103027,
        "y": 2688.190571784973,
        "wires": [
            [],
            []
        ]
    },
    {
        "id": "3b98379f.4f8eb8",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Adequa Dados e Razão",
        "func": "var sete = 7;\nvar busbar_voltage_12 =  ((msg.payload[1]*65536+msg.payload[0])/256);\nvar busbar_voltage_23 =  ((msg.payload[3]*65536+msg.payload[2])/256);\nvar busbar_voltage_31 =  ((msg.payload[5]*65536+msg.payload[4])/256);\nvar generator_voltage_12 =  ((msg.payload[7]*65536+msg.payload[6])/256);\nvar generator_voltage_23 =  ((msg.payload[9]*65536+msg.payload[8])/256);\nvar generator_voltage_31 =  ((msg.payload[11]*65536+msg.payload[10])/256);\nvar current_1 = ((msg.payload[13]*65536+msg.payload[12])/256);\nvar current_2 =  ((msg.payload[15]*65536+msg.payload[14])/256);\nvar current_3 =  ((msg.payload[17]*65536+msg.payload[16])/256);\nvar generator_frequency =  (msg.payload[18]/256);\nvar busbar_frequency =  (msg.payload[19]/256);\n\nvar current_active_power_total =  ((msg.payload[21]*65536+msg.payload[20])/256);\nif(current_active_power_total>8388607){current_active_power_total=current_active_power_total-16777215;}\n\nvar current_reactive_power_total =  ((msg.payload[23]*65536+msg.payload[22])/256);\nif(current_reactive_power_total>8388607){current_reactive_power_total=current_reactive_power_total-16777215;}\n\nvar current_apparent_power_total =  ((msg.payload[25]*65536+msg.payload[24])/256);\n\nvar current_pf_total =  (msg.payload[26]/256);\nif(current_pf_total>8388607){current_pf_total=current_pf_total-16777215;}\n\n//var engine_running_hours =  ((msg.payload[28]*65536+msg.payload[27]));\nvar engine_battery_voltage =  (msg.payload[29]/256);\nvar engine_oil_pressure =  (msg.payload[30]/256);\nvar engine_coolant_temperature =  ((msg.payload[32]*65536+msg.payload[31])/256);\nvar engine_velocity =  (msg.payload[33]);\nvar generator_active_energy =  ((msg.payload[35]*65536+msg.payload[34]));\nvar io_cont_voltage_an_input1_JW =  (msg.payload[36]/256);\nvar io_cont_voltage_an_input2_JW =  (msg.payload[37]/256);\n//ok 0 a 37 = 38\n\nvar engine_intake_manifold1_press =  (msg.payload[38]*1/256 ); //354\nvar engine_throttle_pos =  (msg.payload[39]*1/256 ); //356\nvar engine_intake_manifold1_temp =  ((msg.payload[41]*65536+msg.payload[40])*1/256 ); //359\n//ok 4\n\nvar engine_status = ((msg.payload[42])); \n//ok 1\n\nvar seconds = ((msg.payload[43])); //1\nvar minutes =  ((msg.payload[44])); //2\nvar hours =  ((msg.payload[45])); //3\nvar day_of_month =  ((msg.payload[46])); //4\nvar month =  ((msg.payload[47]));//5\nvar year =  ((msg.payload[48]));//6\nvar engine_working_hours =  ((msg.payload[50]*65536+msg.payload[49]) );//7-8\nvar number_of_cranks = ((msg.payload[52]*65536+msg.payload[51]) );//9-10\nvar engine_working_hours_with_load = ((msg.payload[54]*65536+msg.payload[53]) );//11-12\n\nvar todos = {payload: [\nsete,\nbusbar_voltage_12,\nbusbar_voltage_23,\nbusbar_voltage_31,\ngenerator_voltage_12,\ngenerator_voltage_23,\ngenerator_voltage_31,\ncurrent_1,\ncurrent_2,\ncurrent_3,\ngenerator_frequency,\nbusbar_frequency,\ncurrent_active_power_total,\ncurrent_reactive_power_total,\ncurrent_apparent_power_total,\ncurrent_pf_total,\nengine_battery_voltage,\nengine_oil_pressure,\nengine_coolant_temperature,\nengine_velocity,\ngenerator_active_energy,\nio_cont_voltage_an_input1_JW,\nio_cont_voltage_an_input2_JW,\n\nengine_intake_manifold1_press,\nengine_throttle_pos,\nengine_intake_manifold1_temp,\n\nengine_status,\n\nseconds,\nminutes,\nhours,\nday_of_month,\nmonth,\nyear,\nengine_working_hours,\nnumber_of_cranks,\nengine_working_hours_with_load\n]};\n\n\n\nreturn todos;//msg;\n",
        "outputs": "1",
        "noerr": 0,
        "x": 980.9366912841797,
        "y": 2748.8573803901672,
        "wires": [
            [
                "9b9622b2.c37b7"
            ]
        ]
    },
    {
        "id": "9b9622b2.c37b7",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "INSERIR NO BANCO DE DADOS",
        "func": "msg.topic =\"SET time_zone='America/Sao_Paulo'; INSERT INTO `dados_brasilgtw`.`dados` (`id_dispositivo`,`busbar_voltage_12`,`busbar_voltage_23`,`busbar_voltage_31`,`generator_voltage_12`,`generator_voltage_23`,`generator_voltage_31`,`current_1`,`current_2`,`current_3`,`generator_frequency`,`busbar_frequency`,`current_active_power_total`,`current_reactive_power_total`,`current_apparent_power_total`,`current_pf_total`,`engine_battery_voltage`,`engine_oil_pressure`,`engine_coolant_temperature`,`engine_velocity`,`generator_active_energy`,`io_cont_voltage_an_input1_JW`,`io_cont_voltage_an_input2_JW`,`engine_intake_manifold1_press`,`engine_throttle_pos`,`engine_intake_manifold1_temp`,`engine_status`,`seconds`,`minutes`,`hours`,`day_of_month`,`month`,`year`,`engine_working_hours`,`number_of_cranks`,`engine_working_hours_with_load`) VALUES (\"+msg.payload+\")\";\n\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 1268.651107788086,
        "y": 2742.7301383018494,
        "wires": [
            [
                "2a03d611.26c39a"
            ]
        ]
    },
    {
        "id": "5dd0adf6.cfa704",
        "type": "delay",
        "z": "50f61338.29072c",
        "name": "",
        "pauseType": "delay",
        "timeout": "1",
        "timeoutUnits": "milliseconds",
        "rate": "1",
        "nbRateUnits": "1",
        "rateUnits": "second",
        "randomFirst": "1",
        "randomLast": "5",
        "randomUnits": "seconds",
        "drop": false,
        "x": 149.77783203125,
        "y": 2577.2063241004944,
        "wires": [
            [
                "547da5fd.5476ec",
                "f7f9da5f.0a6458",
                "d8e6404f.64885",
                "c5065a93.3970b8",
                "55fd3067.9139c"
            ]
        ]
    },
    {
        "id": "7be4bb50.ab98f4",
        "type": "catch",
        "z": "50f61338.29072c",
        "name": "",
        "scope": null,
        "x": 406.66662979125977,
        "y": 2851.6666305959225,
        "wires": [
            [
                "d2a25a88.bc3f78"
            ]
        ]
    },
    {
        "id": "70abac89.47fa74",
        "type": "modbus-queue-info",
        "z": "50f61338.29072c",
        "name": "Fila Leitura GMG8 Remoto",
        "unitid": "8",
        "lowLowLevel": 25,
        "lowLevel": 75,
        "highLevel": 150,
        "highHighLevel": 300,
        "server": "986a090a.461d98",
        "errorOnHighLevel": false,
        "x": 983.8889312744141,
        "y": 2845.4444559514523,
        "wires": [
            [
                "32f2c3a3.7364bc"
            ]
        ]
    },
    {
        "id": "d2a25a88.bc3f78",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Reseta leitura se atingir nivel high high",
        "func": "if(\"high high level reached\" === msg.state && \n    msg.unitid === 8 &&\n    msg.error.source.name === \"Read Queue\") {\n    msg.resetQueue = true;\n    return msg;\n}\n",
        "outputs": 1,
        "noerr": 0,
        "x": 667,
        "y": 2849.888871997595,
        "wires": [
            [
                "70abac89.47fa74"
            ]
        ]
    },
    {
        "id": "32f2c3a3.7364bc",
        "type": "debug",
        "z": "50f61338.29072c",
        "name": "",
        "active": false,
        "console": "false",
        "complete": "payload",
        "x": 1220.6986722946167,
        "y": 2846.222205489874,
        "wires": []
    },
    {
        "id": "27aa20b4.e0e01",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Lê 1 a 95 (IR)",
        "func": "msg.payload = { input: msg.payload, 'fc': 4, 'unitid': 7, 'address': 0 , 'quantity': 94 }\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 421.8889694213867,
        "y": 2903.428643077612,
        "wires": [
            [
                "c0fb8c95.2408b"
            ]
        ]
    },
    {
        "id": "c0fb8c95.2408b",
        "type": "modbus-flex-getter",
        "z": "50f61338.29072c",
        "name": "Envia Fila de Leitura GMG8",
        "showStatusActivities": false,
        "showErrors": false,
        "server": "986a090a.461d98",
        "x": 640.4445648193359,
        "y": 2909.428613513708,
        "wires": [
            [
                "4f64cf4e.e777a"
            ],
            []
        ]
    },
    {
        "id": "7d32e34a.217c1c",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Lê 354-359 (IR)",
        "func": "msg.payload = { input: msg.payload, 'fc': 4, 'unitid': 7, 'address': 353 , 'quantity': 7 }\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 425.8889465332031,
        "y": 2952.428592532873,
        "wires": [
            [
                "e59448.e2e12bb8"
            ]
        ]
    },
    {
        "id": "667122d4.b5041c",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Lê 1-25 (HR)",
        "func": "msg.payload = { input: msg.payload, 'fc': 3, 'unitid': 7, 'address': 0 , 'quantity': 26 }\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 418.11121368408203,
        "y": 3048.762009948492,
        "wires": [
            [
                "ea57715d.b2f1d"
            ]
        ]
    },
    {
        "id": "e59448.e2e12bb8",
        "type": "modbus-flex-getter",
        "z": "50f61338.29072c",
        "name": "Envia Fila de Leitura GMG8",
        "showStatusActivities": false,
        "showErrors": false,
        "server": "986a090a.461d98",
        "x": 642.8889465332031,
        "y": 2951.428592532873,
        "wires": [
            [
                "7b6ad396.8cb30c"
            ],
            []
        ]
    },
    {
        "id": "ea57715d.b2f1d",
        "type": "modbus-flex-getter",
        "z": "50f61338.29072c",
        "name": "Envia Fila de Leitura GMG8",
        "showStatusActivities": false,
        "showErrors": false,
        "server": "986a090a.461d98",
        "x": 646.1112060546875,
        "y": 3044.761964648962,
        "wires": [
            [
                "a8f9ad1f.7d374"
            ],
            []
        ]
    },
    {
        "id": "2a06138c.e388ac",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Lê 132 (IR)",
        "func": "msg.payload = { input: msg.payload, 'fc': 4, 'unitid': 7, 'address': 131 , 'quantity': 1 }\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 410.2222595214844,
        "y": 2998.7619055211544,
        "wires": [
            [
                "435eddfd.f1d244"
            ]
        ]
    },
    {
        "id": "435eddfd.f1d244",
        "type": "modbus-flex-getter",
        "z": "50f61338.29072c",
        "name": "Envia Fila de Leitura GMG8",
        "showStatusActivities": false,
        "showErrors": false,
        "server": "986a090a.461d98",
        "x": 637.2222595214844,
        "y": 2997.7619055211544,
        "wires": [
            [
                "c2f37af2.aa51e8"
            ],
            []
        ]
    },
    {
        "id": "97e0b503.387b38",
        "type": "modbus-write",
        "z": "50f61338.29072c",
        "name": "Salva GMG8 Local",
        "showStatusActivities": true,
        "showErrors": true,
        "unitid": "1",
        "dataType": "MHoldingRegisters",
        "adr": "385",
        "quantity": "38",
        "server": "a8d40646.cef038",
        "x": 1108.3334045410156,
        "y": 2907.0953954160213,
        "wires": [
            [],
            []
        ]
    },
    {
        "id": "af15993b.a65188",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Lê GMG8 local",
        "func": "msg.payload = { input: msg.payload, 'fc': 3, 'unitid': 1, 'address': 385 , 'quantity': 55 }\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 447.3176803588867,
        "y": 3093.66682562232,
        "wires": [
            [
                "516d9880.288068"
            ]
        ]
    },
    {
        "id": "516d9880.288068",
        "type": "modbus-flex-getter",
        "z": "50f61338.29072c",
        "name": "Envia Fila de Leitura GMG8 Local",
        "showStatusActivities": false,
        "showErrors": false,
        "server": "a8d40646.cef038",
        "x": 687.1905326843262,
        "y": 3095.8890150487423,
        "wires": [
            [
                "d2f35c95.3813c"
            ],
            []
        ]
    },
    {
        "id": "c677ecc.5d4a41",
        "type": "modbus-write",
        "z": "50f61338.29072c",
        "name": "Salva GMG8 Local",
        "showStatusActivities": true,
        "showErrors": true,
        "unitid": "1",
        "dataType": "MHoldingRegisters",
        "adr": "423",
        "quantity": "4",
        "server": "a8d40646.cef038",
        "x": 1104.246410369873,
        "y": 2952.1589964330196,
        "wires": [
            [],
            []
        ]
    },
    {
        "id": "4f64cf4e.e777a",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Separa Dados",
        "func": "var todos = {payload: [\nmsg.payload[0], //1   busbar_voltage_12 LSB\nmsg.payload[1], //2   busbar_voltage_12 MSB\nmsg.payload[2], //3   busbar_voltage_23 LSB\nmsg.payload[3], //4   busbar_voltage_23 MSB\nmsg.payload[4], //5   busbar_voltage_31 LSB\nmsg.payload[5], //6   busbar_voltage_31 MSB\nmsg.payload[6], //7   generator_voltage_12 LSB\nmsg.payload[7], //8   generator_voltage_12 MSB\nmsg.payload[8], //9   generator_voltage_23 LSB\nmsg.payload[9], //10  generator_voltage_23 MSB\nmsg.payload[10], //11 generator_voltage_31 LSB\nmsg.payload[11], //12 generator_voltage_31 MSB\n\nmsg.payload[20], //13 current_1 LSB\nmsg.payload[21], //14 current_1 MSB\nmsg.payload[22], //15 current_2 LSB\nmsg.payload[23], //16 current_2 MSB\nmsg.payload[24], //17 current_3 LSB\nmsg.payload[25], //18 current_3 MSB\n\nmsg.payload[28], //19 generator_frequency\nmsg.payload[29], //20 busbar_frequency\n\nmsg.payload[60], //21 current_active_power_total LSB\nmsg.payload[61], //22 current_active_power_total MSB\nmsg.payload[62], //23 current_reactive_power_total LSB\nmsg.payload[63], //24 current_reactive_power_total MSB\nmsg.payload[64], //25 current_apparent_power_total LSB\nmsg.payload[65], //26 current_apparent_power_total MSB\n\nmsg.payload[67], //27 current_pf_total\n\nmsg.payload[70], //28 engine_running_hours LSB\nmsg.payload[71], //29 engine_running_hours MSB\n\nmsg.payload[73], //30 engine_battery_voltage\n\nmsg.payload[76], //31 engine_oil_pressure\n\nmsg.payload[77], //32 engine_coolant_temperature LSB\nmsg.payload[78], //33 engine_coolant_temperature MSB\n\nmsg.payload[80], //34 engine_velocity\n\nmsg.payload[85], //35 generator_active_energy LSB\nmsg.payload[86], //36 generator_active_energy MSB\n\nmsg.payload[93], //37 io_cont_voltage_an_input1_JW\nmsg.payload[94]  //38 io_cont_voltage_an_input2_JW\n]};\n\nreturn todos;",
        "outputs": "1",
        "noerr": 0,
        "x": 869.8334350585938,
        "y": 2906.3732403218746,
        "wires": [
            [
                "97e0b503.387b38"
            ]
        ]
    },
    {
        "id": "7b6ad396.8cb30c",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Separa Dados",
        "func": "var todos = {payload: [\nmsg.payload[0], //1 - 354 engine_intake_manifold1_press\n//msg.payload[1], //2 - 355\nmsg.payload[2], //3 - 356 engine_throttle_pos\n//msg.payload[3], //4 - 357\n//msg.payload[4], //5 - 358\nmsg.payload[5], //6 - 359 engine_intake_manifold1_temp LSB\nmsg.payload[6], //7 - 360 engine_intake_manifold1_temp MSB\n]};\n\n\nreturn todos;",
        "outputs": "1",
        "noerr": 0,
        "x": 874.5556945800781,
        "y": 2952.7620647847652,
        "wires": [
            [
                "c677ecc.5d4a41"
            ]
        ]
    },
    {
        "id": "c2f37af2.aa51e8",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Separa Dados",
        "func": "var todos = {payload: [\nmsg.payload[0], //1 - 132\n]};\n\nreturn todos;",
        "outputs": "1",
        "noerr": 0,
        "x": 879.555721282959,
        "y": 2994.2621077001095,
        "wires": [
            [
                "d702f3e0.8185a"
            ]
        ]
    },
    {
        "id": "d702f3e0.8185a",
        "type": "modbus-write",
        "z": "50f61338.29072c",
        "name": "Salva GMG8 Local",
        "showStatusActivities": true,
        "showErrors": true,
        "unitid": "1",
        "dataType": "MHoldingRegisters",
        "adr": "427",
        "quantity": "1",
        "server": "a8d40646.cef038",
        "x": 1101.5560989379883,
        "y": 2995.2621444761753,
        "wires": [
            [],
            []
        ]
    },
    {
        "id": "a8f9ad1f.7d374",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Separa Dados",
        "func": "var todos = {payload: [\nmsg.payload[0], //1   seconds\nmsg.payload[1], //2   minutes\nmsg.payload[2], //3   hours\nmsg.payload[3], //4   day_of_month\n//msg.payload[4], //5 \nmsg.payload[5], //6   month\nmsg.payload[6], //7   year\n//msg.payload[7], //8 \nmsg.payload[8], //9   engine_running_hours LSB\nmsg.payload[9], //10  engine_running_hours MSB\nmsg.payload[10], //11 number_of_cranks LSB\nmsg.payload[11], //12 number_of_cranks MSB\n//0 a 11 foi\nmsg.payload[24], //13 working_hours_with_load LSB\nmsg.payload[25], //14 working_hours_with_load MSB\n]};\n\n//msg.payload = todos.join();\n//msg.topic=1;\n\nreturn todos;",
        "outputs": "1",
        "noerr": 0,
        "x": 884.5557289123535,
        "y": 3040.762109607458,
        "wires": [
            [
                "36d9d2cf.1876fe"
            ]
        ]
    },
    {
        "id": "36d9d2cf.1876fe",
        "type": "modbus-write",
        "z": "50f61338.29072c",
        "name": "Salva GMG8 Local",
        "showStatusActivities": true,
        "showErrors": true,
        "unitid": "1",
        "dataType": "MHoldingRegisters",
        "adr": "428",
        "quantity": "12",
        "server": "a8d40646.cef038",
        "x": 1105.6034889221191,
        "y": 3036.5240019261837,
        "wires": [
            [],
            []
        ]
    },
    {
        "id": "d2f35c95.3813c",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "Adequa Dados e Razão",
        "func": "var oito = 8;\nvar busbar_voltage_12 =  ((msg.payload[1]*65536+msg.payload[0])/256);\nvar busbar_voltage_23 =  ((msg.payload[3]*65536+msg.payload[2])/256);\nvar busbar_voltage_31 =  ((msg.payload[5]*65536+msg.payload[4])/256);\nvar generator_voltage_12 =  ((msg.payload[7]*65536+msg.payload[6])/256);\nvar generator_voltage_23 =  ((msg.payload[9]*65536+msg.payload[8])/256);\nvar generator_voltage_31 =  ((msg.payload[11]*65536+msg.payload[10])/256);\nvar current_1 = ((msg.payload[13]*65536+msg.payload[12])/256);\nvar current_2 =  ((msg.payload[15]*65536+msg.payload[14])/256);\nvar current_3 =  ((msg.payload[17]*65536+msg.payload[16])/256);\nvar generator_frequency =  (msg.payload[18]/256);\nvar busbar_frequency =  (msg.payload[19]/256);\n\nvar current_active_power_total =  ((msg.payload[21]*65536+msg.payload[20])/256);\nif(current_active_power_total>8388607){current_active_power_total=current_active_power_total-16777215;}\n\nvar current_reactive_power_total =  ((msg.payload[23]*65536+msg.payload[22])/256);\nif(current_reactive_power_total>8388607){current_reactive_power_total=current_reactive_power_total-16777215;}\n\nvar current_apparent_power_total =  ((msg.payload[25]*65536+msg.payload[24])/256);\n\nvar current_pf_total =  (msg.payload[26]/256);\nif(current_pf_total>8388607){current_pf_total=current_pf_total-16777215;}\n\n//var engine_running_hours =  ((msg.payload[28]*65536+msg.payload[27]));\nvar engine_battery_voltage =  (msg.payload[29]/256);\nvar engine_oil_pressure =  (msg.payload[30]/256);\nvar engine_coolant_temperature =  ((msg.payload[32]*65536+msg.payload[31])/256);\nvar engine_velocity =  (msg.payload[33]);\nvar generator_active_energy =  ((msg.payload[35]*65536+msg.payload[34]));\nvar io_cont_voltage_an_input1_JW =  (msg.payload[36]/256);\nvar io_cont_voltage_an_input2_JW =  (msg.payload[37]/256);\n//ok 0 a 37 = 38\n\nvar engine_intake_manifold1_press =  (msg.payload[38]*1/256 ); //354\nvar engine_throttle_pos =  (msg.payload[39]*1/256 ); //356\nvar engine_intake_manifold1_temp =  ((msg.payload[41]*65536+msg.payload[40])*1/256 ); //359\n//ok 4\n\nvar engine_status = ((msg.payload[42])); \n//ok 1\n\nvar seconds = ((msg.payload[43])); //1\nvar minutes =  ((msg.payload[44])); //2\nvar hours =  ((msg.payload[45])); //3\nvar day_of_month =  ((msg.payload[46])); //4\nvar month =  ((msg.payload[47]));//5\nvar year =  ((msg.payload[48]));//6\nvar engine_working_hours =  ((msg.payload[50]*65536+msg.payload[49]) );//7-8\nvar number_of_cranks = ((msg.payload[52]*65536+msg.payload[51]) );//9-10\nvar engine_working_hours_with_load = ((msg.payload[54]*65536+msg.payload[53]) );//11-12\n\nvar todos = {payload: [\noito,\nbusbar_voltage_12,\nbusbar_voltage_23,\nbusbar_voltage_31,\ngenerator_voltage_12,\ngenerator_voltage_23,\ngenerator_voltage_31,\ncurrent_1,\ncurrent_2,\ncurrent_3,\ngenerator_frequency,\nbusbar_frequency,\ncurrent_active_power_total,\ncurrent_reactive_power_total,\ncurrent_apparent_power_total,\ncurrent_pf_total,\nengine_battery_voltage,\nengine_oil_pressure,\nengine_coolant_temperature,\nengine_velocity,\ngenerator_active_energy,\nio_cont_voltage_an_input1_JW,\nio_cont_voltage_an_input2_JW,\n\nengine_intake_manifold1_press,\nengine_throttle_pos,\nengine_intake_manifold1_temp,\n\nengine_status,\n\nseconds,\nminutes,\nhours,\nday_of_month,\nmonth,\nyear,\nengine_working_hours,\nnumber_of_cranks,\nengine_working_hours_with_load\n]};\n\n\n\nreturn todos;//msg;\n",
        "outputs": "1",
        "noerr": 0,
        "x": 960.9366683959961,
        "y": 3097.190810531378,
        "wires": [
            [
                "66c3518f.e529d"
            ]
        ]
    },
    {
        "id": "66c3518f.e529d",
        "type": "function",
        "z": "50f61338.29072c",
        "name": "INSERIR NO BANCO DE DADOS",
        "func": "msg.topic =\"SET time_zone='America/Sao_Paulo'; INSERT INTO `dados_brasilgtw`.`dados` (`id_dispositivo`,`busbar_voltage_12`,`busbar_voltage_23`,`busbar_voltage_31`,`generator_voltage_12`,`generator_voltage_23`,`generator_voltage_31`,`current_1`,`current_2`,`current_3`,`generator_frequency`,`busbar_frequency`,`current_active_power_total`,`current_reactive_power_total`,`current_apparent_power_total`,`current_pf_total`,`engine_battery_voltage`,`engine_oil_pressure`,`engine_coolant_temperature`,`engine_velocity`,`generator_active_energy`,`io_cont_voltage_an_input1_JW`,`io_cont_voltage_an_input2_JW`,`engine_intake_manifold1_press`,`engine_throttle_pos`,`engine_intake_manifold1_temp`,`engine_status`,`seconds`,`minutes`,`hours`,`day_of_month`,`month`,`year`,`engine_working_hours`,`number_of_cranks`,`engine_working_hours_with_load`) VALUES (\"+msg.payload+\")\";\n\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 1248.6510848999023,
        "y": 3091.06356844306,
        "wires": [
            [
                "2a03d611.26c39a"
            ]
        ]
    },
    {
        "id": "c117be20.9c535",
        "type": "delay",
        "z": "50f61338.29072c",
        "name": "",
        "pauseType": "delay",
        "timeout": "1",
        "timeoutUnits": "milliseconds",
        "rate": "1",
        "nbRateUnits": "1",
        "rateUnits": "second",
        "randomFirst": "1",
        "randomLast": "5",
        "randomUnits": "seconds",
        "drop": false,
        "x": 129.7778091430664,
        "y": 2925.539754241705,
        "wires": [
            [
                "27aa20b4.e0e01",
                "7d32e34a.217c1c",
                "2a06138c.e388ac",
                "667122d4.b5041c",
                "af15993b.a65188"
            ]
        ]
    },
    {
        "id": "986a090a.461d98",
        "type": "modbus-client",
        "z": "",
        "name": "Remoto",
        "clienttype": "tcp",
        "bufferCommands": true,
        "stateLogEnabled": true,
        "tcpHost": "177.129.113.23",
        "tcpPort": "502",
        "tcpType": "DEFAULT",
        "serialPort": "/dev/ttyUSB",
        "serialType": "RTU-BUFFERD",
        "serialBaudrate": "9600",
        "serialDatabits": "8",
        "serialStopbits": "1",
        "serialParity": "none",
        "serialConnectionDelay": "100",
        "unit_id": "1",
        "commandDelay": "100",
        "clientTimeout": "5000",
        "reconnectTimeout": "5000"
    },
    {
        "id": "20d837e1.532ea8",
        "type": "MySQLdatabase",
        "z": "",
        "host": "brasilgtwdb.cjp5diuol5aj.us-east-2.rds.amazonaws.com",
        "port": "3306",
        "db": "dados_brasilgtw",
        "tz": ""
    },
    {
        "id": "a8d40646.cef038",
        "type": "modbus-client",
        "z": "",
        "name": "Local",
        "clienttype": "tcp",
        "bufferCommands": true,
        "stateLogEnabled": false,
        "tcpHost": "127.0.0.1",
        "tcpPort": "10502",
        "tcpType": "DEFAULT",
        "serialPort": "/dev/ttyUSB",
        "serialType": "RTU-BUFFERD",
        "serialBaudrate": "9600",
        "serialDatabits": "8",
        "serialStopbits": "1",
        "serialParity": "none",
        "serialConnectionDelay": "100",
        "unit_id": "1",
        "commandDelay": "1",
        "clientTimeout": "1000",
        "reconnectTimeout": "2000"
    }
]
