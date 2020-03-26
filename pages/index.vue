
<script>
import logo from "../assets/delete.png"
import drag from "../assets/drag.png"
import setting from "../assets/setting.png"
export default {
  data() {
    return { lines: [0], totalCol: 0, allDiv: [], dragElementId: "" };
  },

  methods: {
    addColumn() {
      let index=this.totalCol++
      this.allDiv.push(
          <div
            class="resizable"
            id={index}
            draggable="true"
            onDrag={this.onDragStart}
          >
          <img class="logo display btn dlt-btn" onClick={this.deleteDiv} id={index} src={logo} />
         <img class="btn display" id={index} src={drag}/>
         <img src={setting} class="display text-btn" id={index} onClick={this.input}/>
          <textarea class="textarea" placeholder="type something" id={"txt"+index}/>
          </div>
        );
      
    },
    input(ele){
      let elemnt=document.getElementById("txt"+ele.target.id)
      
      elemnt.style.display=(elemnt.style.display=="block")?"none":"block"
    },
    onDragStart(event) {
      this.dragElementId = event.target.id;
    },
    onDragOver(event) {
      event.preventDefault();
    },

    onDrop(event) {
      console.log("called");
      
      const draggableElement = document.getElementById(this.dragElementId);
      this.setTranslate(event.offsetX, event.offsetY, draggableElement);
    },
    
    setTranslate(xPos, yPos, el) {
      el.style.position = "fixed";
      el.style.left = xPos + "px";
      el.style.top = yPos + "px";
    },

    deleteDiv(ele){
      let id=Number(ele.target.id);
      for (let index = 0; index < this.allDiv.length; index++) {
        if (this.allDiv[index].data.attrs.id==id) {
          this.allDiv.splice(index,1)
        }
        
      }      
    }
  },
  render(h) {
    return (
      <div
        class="container"
        onDragover={this.onDragOver}
        onDrop={this.onDrop}
      >
        <button onClick={this.addColumn}>add</button>
        {this.allDiv}
      </div>
    );
  }
};
</script>