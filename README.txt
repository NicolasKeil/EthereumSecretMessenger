To run this code succesfully, to see how the code is working and to see how the Blockchain responds, 
we need to connect the IDE with Ganache. In addition we need to deploy our Smart Contract in Remix to 
the Ganache Blockchain.



<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Deploy a Remix Contract</title>

    <link rel="stylesheet" type="text/css" href="main.css">

    <script src="https://cdn.jsdelivr.net/gh/ethereum/web3.js/dist/web3.min.js"></script>
</head>

<body>
    <div>
        <h1>Ethereum Secret Messenger</h1>
        <hr>

        <label for="message">
            This site writes a secret message to the Ethereum
            blockchain!
        </label>
        <input id="userInput" type="text">

        <button id="setMessageButton">Set secret message</button>
        <button class="enableEthereumButton">Enable Ethereum</button>
    </div>

    <script src="https://code.jquery.com/jquery-3.2.1.slim.min.js"></script>

    <script>

        // Connect a the web3 provider
        if (typeof web3 !== 'undefined') {
            web3 = new Web3(window.ethereum);
            console.log("meta!!!!!!")
        } else {
            web3 = new Web3(new Web3.providers.HttpProvider("https://goerli.infura.io/v3/53c2790a31194eb8a7c0b93ec9f8ff1e"));
        }

        // Set a default account
        web3.eth.defaultAccount = web3.eth.accounts[0];

        // Get the contract address
        /* What is different from the other code:
         * Here we used web3.eth.Contract in the correct and newer form.
         * This method from the library might got updated so we are calling
         * the ABI and the Smart Contract Address with one method
         */

        
        var RemixContract = new web3.eth.Contract(
            [
                {
                    "constant": false,
                    "inputs": [
                        {
                            "name": "x",
                            "type": "string"
                        }
                    ],
                    "name": "setMessage",
                    "outputs": [],
                    "payable": false,
                    "stateMutability": "nonpayable",
                    "type": "function"
                },
                {
                    "constant": true,
                    "inputs": [],
                    "name": "getMessage",
                    "outputs": [
                        {
                            "name": "",
                            "type": "string"
                        }
                    ],
                    "payable": false,
                    "stateMutability": "view",
                    "type": "function"
                }
            ], '0x5Ed6aeD7caeC16470E56bC9303578548F3F8A4C2', {
                from: '0x859D8CDCD539d1836c9536259939Ce199Be03a16', // default from address
                gasPrice: '20000000000' // default gas price in wei, 20 gwei in this case
        }
        );
        

        /*
        var RemixContract = [
            {
                "constant": false,
                "inputs": [
                    {
                        "name": "x",
                        "type": "string"
                    }
                ],
                "name": "setMessage",
                "outputs": [],
                "payable": false,
                "stateMutability": "nonpayable",
                "type": "function"
            },
            {
                "constant": true,
                "inputs": [],
                "name": "getMessage",
                "outputs": [
                    {
                        "name": "",
                        "type": "string"
                    }
                ],
                "payable": false,
                "stateMutability": "view",
                "type": "function"
            }
        ];
*/

        /*
        // Get the contract abi
        var myMessage = new web3.eth.Contract(RemixContract, '0x5Ed6aeD7caeC16470E56bC9303578548F3F8A4C2');
        console.log(myMessage);
*/

        /*
        $("#setMessageButton").click(function () {
            RemixContract.methods.setMessage($("#userInput").val()).send();
            console.log($("#userInput").val())
        });
        */
        

        /*
        $("#setMessageButton").click(function () {
            message = $("#userInput").val()
            myMessage.methods.setMessage(message, (error, result) => { message = result });
            console.log($("#userInput").val())
        });
        */

        
       // Linked to Frontend Set Message Button - which creates a transaction on blockchain
    $("#setMessageButton").click(function () {
        message = $("#userInput").val()
        RemixContract.methods.setMessage(message).send() //{ from: '0x859D8CDCD539d1836c9536259939Ce199Be03a16' }
        console.log($("#userInput").val())
    });



        /*
        const ethereumButton = document.querySelector('.enableEthereumButton');

        ethereumButton.addEventListener('click', () => {
            //Will Start the metamask extension
            ethereum.request({ method: 'eth_requestAccounts' });
        });
        */
    </script>
</body>

</html>



