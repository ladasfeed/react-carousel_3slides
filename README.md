# react-carousel_3slides
Hello everyone! I made a carousel slider when you see three slides.
To use that you should dowloand hook useCarouselSlider and create component wrapper for our slider. If you want to your slider work correctly please don't
touch useCarouselSlider and follow the rules below.
1. Structure of slider wrapper: define array of refs outside the component, typing component according to example, define refs as many as you have slides, 
useEffect and assign array of our refs to var which we defined above, and call hook (it will returns controller). Dont touch class names, but you can modify wrapper
class name to determinate width and height. 
Honestly you can copy code below and change count of slides and jsx(define slides and contorllers).
    
        import useSliderController from './useCarouselSlider';

        let arrayOfSlides:Array<RefObject<HTMLDivElement>> = [] //define array of refs to our slides

        type CarouselSliderType = {
            tempSlide: number,
            setTempSlide: (value: number) => void,
            onMouseSlide: number, //it allows to switch slides onClick or onMouseEnter on specific elems, that prop you can make optional
            transformActive: string //css value of transform for middle element
        }

        const CarouselSlider:React.FC<CarouselSliderType> = ({tempSlide, setTempSlide, onMouseSlide, transformActive}) => {

            //that strings don't look so beautiful, but now i dont know how to make readble array of refs
            const sldie_1 = useRef<HTMLDivElement>(null)
            const sldie_2 = useRef<HTMLDivElement>(null)
            const sldie_3 = useRef<HTMLDivElement>(null)
            const sldie_4 = useRef<HTMLDivElement>(null)
            const sldie_5 = useRef<HTMLDivElement>(null)
            const sldie_6 = useRef<HTMLDivElement>(null)
            const sldie_7 = useRef<HTMLDivElement>(null)

            //effect will work once when component will rendered first
            useEffect(() => {
                arrayOfSlides = [sldie_1, sldie_2, sldie_3, sldie_4, sldie_5, sldie_6, sldie_7]
            }, [0])

            //here we use our hook, it returns funtion to control current slide. It takes boolean, depends on vector
            const sliderController = useSliderController({
                tempSlide,
                setTempSlide,
                arrayOfSlidersLocal: arrayOfSlides,
                onMouseSlide, //give to hook number to determinate which slide we want to see now
                transformActive,
                length: arrayOfSlides.length
            })

            return (
            <>
                <div className="carousel-wrapper">
                    //determinate slider with ref, you can try to do that with map
                    <div className="carousel-slider">
                        <div ref={sldie_1} className="carousel-slide">
                            1
                        </div>
                        <div ref={sldie_2}  className="carousel-slide">
                            2
                        </div>
                        <div ref={sldie_3} className="carousel-slide">
                            3
                        </div>
                        <div ref={sldie_4} className="carousel-slide">
                            4   
                        </div>
                        <div ref={sldie_5} className="carousel-slide">
                            5   
                        </div>
                        <div ref={sldie_6} className="carousel-slide">
                            6   
                        </div>
                        <div ref={sldie_7} className="carousel-slide">
                            7  
                        </div>
                    </div>


                </div>

                <div className='carousel-control'>
                    <div className="controller2" onClick={()=>sliderController(false)}>Prev</div>
                    <div className="controller1" onClick={()=>sliderController(true)}>Next</div>
                </div>
            </>
            )
        }
        export default CarouselSlider
        
 2. Page with carousel. Define tempSlide state, onMouseSlide state (here you can control slides outside SliderCompontent), define function which will 
 setOnMouseSlide( needed slide ). 
 
            const CarouselSliderPage = () => {
              const [tempSlide, setTempSlide] = useState(1)
              const [onMouseSlide, setOnMouseSlide] = useState(1)
              //define onMouseEnter function
              const onMouseSlider = (event: React.MouseEvent<HTMLElement>) => {
                  setOnMouseSlide(parseInt((event.target as HTMLInputElement).id))
              }


              return (
                  <div>
                      <Slider
                          tempSlide={tempSlide}
                          setTempSlide={setTempSlide}
                          onMouseSlide={onMouseSlide}
                          transformActive="scale(1.3)"
                      />
                      <div className="hovers">
                          <div id='1' onMouseEnter={onMouseSlider}>1</div>
                          <div id='2' onMouseEnter={onMouseSlider}>2</div>
                          <div id='3' onMouseEnter={onMouseSlider}>3</div>
                          <div id='4' onMouseEnter={onMouseSlider}>4</div>
                          <div id='5' onMouseEnter={onMouseSlider}>5</div>
                          <div id='6' onMouseEnter={onMouseSlider}>6</div>
                          <div id='7' onMouseEnter={onMouseSlider}>7</div>
                      </div>
                  </div>
            )
        }
