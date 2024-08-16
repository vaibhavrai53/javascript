let boxes = document.querySelectorAll(".box");
let resetbtn = document.querySelector("#reset-btn");
let newgamebtn = document.querySelector("#new-btn");
let msgcontainer = document.querySelector(".msg-container");
let msg = document.querySelector("#msg");

let turno=true;//player x,o

const winpatterns =[
    [0,1,2],
    [0,3,6],
    [0,4,8],
    [1,4,7],
    [2,5,8],
    [2,4,6],
    [3,4,5],
    [6,7,8]
];
const resetgame = () =>{
     turno=true;
     enablewinner()
     msgcontainer.classList.add("hide");
};




boxes.forEach((box) => {
    box.addEventListener("click", () => {
        console.log("box was clicked");
        if(turno===true){
            box.innerText="O";
            turno=false;
        }else{
            box.innerText="X";
            turno=true;
        }
        box.disabled=true;

        checkwinner();
    
})
});

const disablewinner = () =>
{
    for(let box of boxes){
        box.disabled=true;
    }

};
const enablewinner = () =>
    {
        for(let box of boxes){
            box.disabled=false;
            box.innerText="";
        }
    
    };

const showwinner = (winner) =>{
       msg.innerText = `congvrats,winner is ${winner}`;
       msgcontainer.classList.remove("hide");
       disablewinner();
};

const checkwinner = () =>{
    for(let pattern of winpatterns){
            let pos1val= boxes[pattern[0]].innerText,
              pos2val= boxes[pattern[1]].innerText,
              pos3val= boxes[pattern[2]].innerText

    if(pos1val !="" && pos2val !="" && pos3val !="") {
        if(pos1val===pos2val && pos2val===pos3val){
            console.log("winner",pos1val);
            showwinner(pos1val);
        }
    }      
      
    };
};

newgamebtn.addEventListener("click", resetgame);
resetbtn.addEventListener("click",resetgame);
